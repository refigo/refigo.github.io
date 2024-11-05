---
title: NVIDIA Jetpack 6.0에서 RealSense D455f 장치 인식 문제 및 해결
date: 2024-10-17
categories: [IoT, Jetson]
tags: [NVIDIA, Jetson]
---

# 요약

- **문제점**: JetPack 6.0이 설치된 NVIDIA Jetson Orin (AGX와 NX 둘 다)에서 **Python** 및 **ROS2 wrapper**로 **D455f 카메라**를 실행하려 했으나 **장치를 찾을 수 없다는 에러**가 발생함.
    - 하지만, **realsense-viewer**(RealSense2 SDK 도구)에서는 카메라가 인식되고 영상 스트림이 잘 수신됨.
    - **D435 카메라**는 정상적으로 작동하였음 (IMU가 없는 모델).
- **해결 방법**: **JetPack 버전을 6.0에서 5.1로 다운그레이드**한 후 시스템을 다시 플래시함.
    - 이후 `apt install`을 통해 **RealSense2 SDK**와 **ROS2 wrapper**를 설치하니 문제없이 D455f 카메라 이미지와 IMU 데이터를 ROS2 토픽으로 확인할 수 있었음.
- **결론**: 당분간 **JetPack 5.1**을 사용하고, JetPack 6.0에서 공식적인 IMU 지원이 추가될 때까지 기다리는 것을 추천.
    - **libuvc backend**로 빌드하고 **커널 패치**를 시도해서 해결해 볼 수도 있겠으나,
        - libuvc backend는 **개발용**으로만 권장되며, 프로덕션 환경에서는 비권장.
        - 커널 패치 작업은 보드마다 맞춤형으로 필요하므로 복잡함.
        - 특히 현재 사용하는 Jetson NX의 경우 **J401 보드를 사용 (Seeed 제품)**
            - NVIDIA 공식 커널 버전이 아니므로 커널 패치가 작동하지 않을 가능성이 높음.
    - 이러한 작업은 시간이 오래 걸리고 유지보수가 어려워, 공식 지원이 나올 때까지 JetPack 5.1을 사용하는 것이 더 효율적임.

# 본 내용

NVIDIA Jetpack 6.0(Jetson Orin Series)에서 **RealSense D455f** 카메라가 Python 및 ROS2 wrapper에서 인식되지 않는 문제를 발견하였습니다. (문제 발견 시점: 2024-10-14)

해당 문제의 원인, 시도한 해결 방법, 최종 해결책 등을 정리하여 Jetson과 RealSense 통합 작업 시 발생할 수 있는 유사한 문제에 대비할 수 있도록 트러블 슈팅 과정을 기록합니다.

## 문제 상황

- **문제점**: JetPack 6.0이 설치된 NVIDIA Jetson Orin (AGX, NX)에서 **Python** 및 **ROS2 wrapper**로 **D455f 카메라**를 실행하려 했으나 **장치를 찾을 수 없다는 에러**가 발생함.
    - 하지만, **realsense-viewer**(RealSense2 SDK 도구)에서는 카메라가 인식되고 영상 스트림이 잘 수신됨.
    - **D435 카메라**는 정상적으로 작동하였음.
- 해당 문제 발생 화면

![해당 문제 발생 화면](/posts/20241017/image.png)

## **원인 파악**

- **JetPack 6.0**의 리눅스 커널에 D455와 같은 **IMU를 포함한 장치**(HID 장치)를 위한 드라이버가 기본적으로 지원되지 않음이 문제의 원인으로 파악됨.
    - **HID 장치** 드라이버(예: **hidraw**)가 JetPack 6.0에 포함되지 않아 D455f 인식에 문제가 발생.
- D455 시리즈의 경우 모든 모델이 IMU가 장착된 것으로 파악 (아래 도표 참고)
    - IMU가 없는 **D435** 모델은 이 문제의 영향을 받지 않음.

![d455-imu](/posts/20241017/image-1.png)

## **해결 방안 및 시도한 방법**

### **시도 1: librealsense SDK를 LibUVC backend로 빌드 시도 (실패)**

- libuvc backend를 사용해 커널 의존성을 우회하여 librealsense SDK를 빌드.
- 아래는 libuvc 설치 가이드

    [LibUVC-backend installation](https://github.com/IntelRealSense/librealsense/blob/master/doc/libuvc_installation.md)

- 결과: 여러 차례 시도했으나 동일한 에러가 발생, 문제 해결 실패.

### **시도 2: 공식 커널에 MIPI 드라이버 패치 빌드 시도 (실패)**

- Jetpack 6.0 커널에 realsense에서 제공하는 MIPI 드라이버 패치하여 빌드

    [realsense_mipi_platform_driver/README_JP6.md at dev · IntelRealSense/realsense_mipi_platform_driver](https://github.com/IntelRealSense/realsense_mipi_platform_driver/blob/dev/README_JP6.md#build-environment-prerequisites)

- 자동 스크립트로 커널 다운로드 시 시간이 지나치게 오래 걸림.
    - 1시간에 0.8% 추정의 속도로 진행
- 결과: 수동으로 패치하여 재부팅 후, USB 키보드/마우스 동글이 인식되지 않아 조작 불가 상태가 됨
    - Jetson OS를 다시 플래시해야 했음.

### **시도 3: libuvc backend 빌드 + 커널 패치 (중단)**

- 시도 1과 2 동시에 적용하기 위해 재시도.
- 자동 스크립트로 커널을 다운로드하며 기다리는 동안 다른 해결책(시도 4)을 병행.
- 시도 4 방법(JetPack 5.1로 다운그레이드)이 성공하여, 커널 패치 및 libuvc 빌드 시도를 중단함.

### **시도 4: JetPack 5.1로 다운그레이드 (성공)**

- **JetPack 5.1**로 시스템을 다시 플래시한 후 `apt install` 명령어로 **RealSense SDK**와 **ROS2 wrapper** 설치.
- JetPack 5.1 플래시는 아래 문서 참고
    - [Flash Jetpack - Seeed Studio Wiki](https://wiki.seeedstudio.com/reComputer_J4012_Flash_Jetpack/#flash-jetpack)
	
    - 단, JetPack 5의 경우 Host PC가 Ubuntu 20.04 버전이어야 설치 가능 (Ubuntu 22.04에서 불가).
    
- **결과**:
    - D455f 카메라가 Python, ROS2로 정상 인식되고, IMU 데이터도 ROS2 토픽에서 확인 가능.
    - 추가적인 패치나 수동 작업 없이도 정상 작동.

## **결론**

JetPack 6.0에서 **IMU를 포함한 D455f 카메라**를 사용하는 것은 현재로선 쉽지 않습니다. **libuvc backend 빌드**나 **커널 패치**로 문제를 해결할 수도 있지만, 이는 복잡하고 안정성이 부족합니다.

무조건 JetPack 6.0을 사용해야하는 상황이 아니라면 현재 **JetPack 5.1으로 다운그레이드**하는 것이 가장 간단하고 확실한 해결책입니다. 이는 Jetson 환경에서 안정적으로 RealSense 카메라를 사용할 수 있도록 하며, JetPack 6 환경에서 IMU 지원이 공식적으로 추가될 때까지는 이 방법을 권장합니다.

## **대표 참고 자료**

- **Intel RealSense 커뮤니티 논의**:
    
    [cannot connect D455 on jetson agx orin](https://support.intelrealsense.com/hc/en-us/community/posts/31576776977427-cannot-connect-D455-on-jetson-agx-orin?page=1#community_comment_31577939626771)
    
    - IMU가 있는 RealSense 카메라는 JetPack 6.0에서 MIPI 드라이버가 필요.
    - libuvc backend를 사용하면 커널 의존성을 우회하여 복잡한 커널 패치 작업을 피할 수 있지만, 성능적 및 확장성 측면으로 한계가 있음.
    - JetPack 5.1로 다운그레이드하는 것이 일반적인 해결책으로 추천됨.

# 관련 이슈 모음집

[Realsense D455 IMU not working in JP6](https://forums.developer.nvidia.com/t/realsense-d455-imu-not-working-in-jp6/303447)

[Connecting Intelrealsense Depth Camera D455 to Jetson Orin Nano 8GB](https://forums.developer.nvidia.com/t/connecting-intelrealsense-depth-camera-d455-to-jetson-orin-nano-8gb/296753)

[D435I not use camera when use IMU](https://forums.developer.nvidia.com/t/d435i-not-use-camera-when-use-imu/305622)

[Jetson Orin NX - librealsense 2.55.1 - D455 - color frame drop 80%, IMU doesn't work · Issue #13020 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/13020#top)

[Support for Intel RealSense IMU cameras (e.g. D435i) on Jetpack 6?](https://forums.developer.nvidia.com/t/support-for-intel-realsense-imu-cameras-e-g-d435i-on-jetpack-6/303774)

[cannot connect D455 on jetson agx orin](https://support.intelrealsense.com/hc/en-us/community/posts/31576776977427-cannot-connect-D455-on-jetson-agx-orin?page=1#community_comment_31577939626771)

[RealSense D456 not working on Jetson Orin Nano with ROS2 packages · Issue #12831 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/12831#top)

[D435i on Jetson Orin Nano (No devices found) · Issue #3015 · IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros/issues/3015#top)

[jetson orin AGX issues after upgrading to jetpack 6.0 · Issue #3185 · IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros/issues/3185#top)

[RealSense D456 not working on Jetson Orin Nano with ROS2 packages · Issue #12831 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/12831#top)

[HIDRAW on jetson nano](https://forums.developer.nvidia.com/t/hidraw-on-jetson-nano/285961)

[Jetson 6.0DP and "No Device Detected" in Python only · Issue #12807 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/12807#top)

[Support for D435i (IMU) cameras with the MIPI driver on Jetson Orin NX with Jetpack 6 · Issue #228 · IntelRealSense/realsense_mipi_platform_driver](https://github.com/IntelRealSense/realsense_mipi_platform_driver/issues/228#top)

[Jetson Orin with Jetpack 6.0 · Issue #12566 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/12566#top)

[Running pyrealsense2 on JetsonNano · Issue #6964 · IntelRealSense/librealsense](https://github.com/IntelRealSense/librealsense/issues/6964#top)

[Can not get imu data (realsense D455, Jetson nano) · Issue #2212 · IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros/issues/2212#top)

[IMU Sensor Model Detection in D455](https://support.intelrealsense.com/hc/en-us/community/posts/4409300648595-IMU-Sensor-Model-Detection-in-D455)
