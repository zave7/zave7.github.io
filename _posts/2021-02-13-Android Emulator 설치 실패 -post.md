---
title: "Android Emulator AMD 설치 실패"
categories: Android
---

# # AMD
## - 원인
  - CPU가 AMD라서..

## - 해결 방법
  - 사전작업 : 윈도우라면 Hyper-V 를 완전히 비활성화 시켜야한다.
  1. https://github.com/google/android-emulator-hypervisor-driver-for-amd-processors 에 접속
  2. Releases 에서 최신 버전 zip 파일 다운로드
  3. 압축 해제 후 관리자 권한으로 명령 프롬프트 실행
  4. 모듈 내에 있는 silent_install.bat 실행
  5. 결과  
      - 상태에서 4 RUNNING 이 나와야 한다.  
    ![GitHub Logo](/images/android/gvm_emulator.png){: width="100%" height="100%"}

# # Intel

## - 원인
  - hyper-v 가 활성화 되어있어서
  - This computer does not support Intel Virtualization Technology (VT-x) or it is being exclusively used by Hyper-V. HAXM cannot be installed. 
Please ensure Hyper-V is disabled in Windows Features, or refer to the Intel HAXM documentation for more information.

## - 해결 방법
  - hyper-v 비활성화
