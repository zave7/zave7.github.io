# Android Emulator AMD 설치 실패

## 원인
  - CPU가 AMD라서..

## 해결 방법
  - 사전작업 : 윈도우라면 Hyper-V 를 완전히 비활성화 시켜야한다.
  1. https://github.com/google/android-emulator-hypervisor-driver-for-amd-processors 에 접속
  2. Releases 에서 최신 버전 zip 파일 다운로드
  3. 압축 해제 후 관리자 권한으로 명령 프롬프트 실행
  4. 모듈 내에 있는 silent_install.bat 실행
  5. 결과
    ![GitHub Logo](/images/android/gvm_emulator.png){: width="50%" height="50%"}
