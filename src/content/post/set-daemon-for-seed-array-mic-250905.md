---
title: "Set daemon for seeed respeaker array mic as input device"
publishDate: "27 January 2023"
description: "An example post for Astro Cactus, detailing how to add a custom social image card in the frontmatter"
tags: ["example", "blog", "image"]
ogImage: "/social-card.png"
---

ReSpeaker(Seeed) 마이크가 기본 입력 장치가 아니면 자동으로 바꿔주는 스크립트와, 이를 5분 주기로 실행하는 systemd **user** 타이머 구성입니다. (마이크/오디오 컨트롤은 보통 **사용자 세션**에서 동작하므로 root system 서비스보다 _user 서비스_가 안전합니다.)

# 1) 스크립트 (/usr/local/bin/check_seeed_mic.sh)

```bash
#!/usr/bin/env bash
# check_seeed_mic.sh
# Ubuntu 22.04, PipeWire/Pulse 공통. 기본 입력(source)이 Seeed ReSpeaker가 아니면 자동 설정.

set -euo pipefail

# 원하는 소스 식별 키워드 (필요시 조정)
PREFERRED_MATCH="usb-SEEED_ReSpeaker_4_Mic_Array__UAC1.0_-00.multichannel-input"

log() {
  logger -t check_seeed_mic "[INFO] $*"
  echo "[INFO] $*"
}

err() {
  logger -t check_seeed_mic "[ERROR] $*"
  echo "[ERROR] $*" >&2
}

# pactl 가용성 확인
if ! command -v pactl >/dev/null 2>&1; then
  err "pactl not found. Install pulseaudio-utils or pipewire-pulse."
  exit 1
fi

# 현재 기본 소스 확인
CURRENT_DEFAULT="$(pactl info 2>/dev/null | awk -F': ' '/Default Source:/ {print $2}')"

# 사용 가능한 소스 목록(짧은 형식)
AVAILABLE_SOURCES="$(pactl list sources short | awk '{print $2}')"

# 선호 소스 후보 찾기 (정확명 우선, 없으면 유사 패턴 검색)
CANDIDATE="$(echo "$AVAILABLE_SOURCES" | grep -E "^${PREFERRED_MATCH}$" || true)"
if [[ -z "$CANDIDATE" ]]; then
  # 혹시 장치명이 약간 다를 수도 있으니 폭넓게 검색 (ReSpeaker, multichannel-input 조합)
  CANDIDATE="$(echo "$AVAILABLE_SOURCES" | grep -i 'usb-SEEED_ReSpeaker' | grep -i 'multichannel-input' || true)"
fi

if [[ -z "$CANDIDATE" ]]; then
  err "Seeed ReSpeaker source not found in available sources."
  err "Available: $(echo "$AVAILABLE_SOURCES" | tr '\n' ' ')"
  exit 0  # 장치 미연결일 수 있으니 실패로 취급하지 않음
fi

if [[ "$CURRENT_DEFAULT" == "$CANDIDATE" ]]; then
  log "Default source already set to '$CANDIDATE'. Nothing to do."
  exit 0
fi

# 기본 소스 설정
if pactl set-default-source "$CANDIDATE"; then
  log "Set default source to '$CANDIDATE'."
else
  err "Failed to set default source to '$CANDIDATE'."
  exit 1
fi

# 현재 녹음 중인 스트림(source-outputs)을 새 소스로 이동 (있을 때만)
# 목록 형식: index  source  client  sample_format  channel_map  corked  latency  resample_method  properties
while read -r LINE; do
  [[ -z "$LINE" ]] && continue
  IDX="$(echo "$LINE" | awk '{print $1}')"
  if pactl move-source-output "$IDX" "$CANDIDATE" 2>/dev/null; then
    log "Moved source-output $IDX to '$CANDIDATE'."
  fi
done < <(pactl list short source-outputs 2>/dev/null || true)

exit 0
```

권한 부여:

```bash
sudo install -m 0755 check_seeed_mic.sh /usr/local/bin/check_seeed_mic.sh
```

> 기본 장치명이 예시와 다르면 `PREFERRED_MATCH` 값을 `pactl list sources short` 결과에 맞게 바꿔주세요.

---

# 2) systemd **user** 서비스/타이머

## 서비스 파일 (~/.config/systemd/user/seeed-mic-check.service)

```ini
[Unit]
Description=Check & set Seeed microphone as default input

[Service]
Type=oneshot
ExecStart=/usr/local/bin/check_seeed_mic.sh
# pactl은 사용자 세션의 Pulse/ PipeWire에 붙으므로 user 서비스가 적합
```

## 타이머 파일 (~/.config/systemd/user/seeed-mic-check.timer)

```ini
[Unit]
Description=Run seeed-mic-check every 5 minutes

[Timer]
OnBootSec=1min
OnUnitActiveSec=5min
Unit=seeed-mic-check.service
Persistent=true

[Install]
WantedBy=timers.target
```

설치/활성화:

```bash
# user 단위 디렉토리 생성
mkdir -p ~/.config/systemd/user

# 위 두 파일 저장 후:
systemctl --user daemon-reload
systemctl --user enable --now seeed-mic-check.timer

# 동작 확인
systemctl --user list-timers | grep seeed-mic-check
journalctl --user -u seeed-mic-check.service -f
```

---

## (선택) root(system) 타이머로 돌려야 하는 상황일 때

`pactl`는 **해당 사용자 세션**의 Pulse/PipeWire에 붙어야 합니다. 불가피하게 system 단위에서 실행하려면, 환경을 사용자의 런타임으로 넘겨야 합니다(예: 사용자 `xyz-ai`, UID는 `id -u xyz-ai`로 확인):

`/etc/systemd/system/seeed-mic-check.service`

```ini
[Unit]
Description=Check & set Seeed microphone (system -> user runtime)
After=network.target

[Service]
Type=oneshot
User=xyz-ai
Environment=XDG_RUNTIME_DIR=/run/user/1000
ExecStart=/usr/local/bin/check_seeed_mic.sh
```

`/etc/systemd/system/seeed-mic-check.timer`

```ini
[Unit]
Description=Run seeed-mic-check every 5 minutes (system)

[Timer]
OnBootSec=1min
OnUnitActiveSec=5min
Unit=seeed-mic-check.service
Persistent=true

[Install]
WantedBy=timers.target
```

적용:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now seeed-mic-check.timer
sudo systemctl status seeed-mic-check.timer
```

---

## 빠른 수동 테스트

```bash
/usr/local/bin/check_seeed_mic.sh
pactl info | grep "Default Source"
pactl list sources short
```

이 구성으로 5분마다 ReSpeaker가 연결되어 있고 기본 입력이 아니라면 자동으로 `set-default-source` 되고, 녹음 중인 스트림도 가능한 한 새 소스로 이동됩니다. 필요 시 `PREFERRED_MATCH`만 딱 한 번 여러분 시스템의 실제 장치명에 맞춰 조정해 주세요.
