# Feature: 다국어(i18n) 지원 완성

## 요약
최근 커밋(b389545)에서 다국어 구조 리팩토링이 시작됐으나, 아직 미완성 상태.

## 현재 상태
- `ros-mcp-server-camera-practice-20251125/` 포스트가 `ko.md`만 존재 (영문 버전 없음)
- `site.config.ts`의 `lang`, `ogLocale`이 `en-GB`로 하드코딩
- 언어별 라우팅 미구현 (e.g., `/ko/...`, `/en/...`)

## 요구사항
- [ ] 언어별 라우팅 구현 (`/ko/`, `/en/` 등)
- [ ] 기존 콘텐츠에 대한 기본 언어 버전 생성
- [ ] `site.config.ts`에 다국어 설정 추가
- [ ] Astro i18n 기능 또는 `@astrojs/i18n` 활용 검토

## 참고
- Astro 공식 i18n 문서: https://docs.astro.build/en/guides/internationalization/
- 현재 콘텐츠 구조: `src/content/post/[slug]/ko.md` 패턴 시작됨
