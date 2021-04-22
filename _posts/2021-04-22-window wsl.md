---
title: window wsl2 설치
categories: Win-Tool
---

# - WSL
- WSL : Windows Subsystem for Linux
    - 윈되우 10에서 네이트브로 리눅스 실행파일을 실행하기 위한 호환선 계층이다.
    - 윈도우에서 리눅스를 사용하기 위한 도구라고 보면된다.

## 1. WSL1 과 WSL2
- `WSL2`는 기존과 다른 vm 환경을 갖고있다.
- `WSL1`에서 Linux의 System Call을 Windows API로 변환하는 구조였다고 하면, `WSL2`에서는 윈도우즈에 리눅스 커널을 아예 올려버렸다고 한다.
- `WSL1`이 윈도우위 api를 이용하기 위하여 변환과정을 거쳤기 때문에, 속도적인 측면에서 불리하였고 일부 API 는 변환이 불가능했다.
- `WSL2`는 Linux 커널을 포함하고 있기 때문에, Linux의 모든 API를 지원한다.

## 2. WSL2 설치
### 1) Windows Terminal 설치
- windows store에서 terminal을 검색 후 설치

### 2) WSL2 활성화 명령어 실행
- WSL feature enable
    ```
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```
- Virtual Machine Platform feature Enable
    ```
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```
    
### 3) window store 에서 원하는 리눅스 버전 설치
- 지원하는 리눅스 버전
    - Ubuntu 16.04 LTS
    - Ubuntu 18.04 LTS
    - Ubuntu 20.04 LTS
    - openSUSE Leap 15.1
    - SUSE Linux Enterprise Server 12 SP5
    - SUSE Linux Enterprise Server 15 SP1
    - Kali Linux
    - Debian GNU/Linux
    - Fedora Remix for WSL
    - Pengwin
    - Pengwin Enterprise
    - Alpine WSL

### 4) WSL2로 변환
- 설치한 Linux 배포에 할당된 WSL 버전 확인
    ```
    wsl --list --verbose
    ```
    - `wsl1` 일 경우
        ```
          Name           State         Version
        * Ubuntu         Running       1
        ```
- 해당 버전을 WSL2로 만들기
    ```
    wsl --ser-version <distribution name> <versionNumber>
    # ex) wsl --ser-version Ubuntu 2
    ```
- WSL2를 기본 버전으로 설정
    ```
    wsl --set-default-version 2
    ```
- 변환 완료
    - 아래와 같은 메세지가 출력된다
        ```
        변환이 진행 중입니다. 몇 분 정도 걸릴 수 있습니다...
        WSL 2와의 주요 차이점에 대한 자세한 내용은 https://aka.ms/wsl2를 참조하세요
        변환이 완료되었습니다.
        ```
- 적용된 버전 확인
    ```
    wsl --list --verbose
    ```
    - 결과
        ```
          Name           State         Version
        * Ubuntu         Running       2
        ```
    - 위와 깉이 나오지 않을 때 wsl을 재부팅 후 확인
        ```
        wsl -r Ubuntu
        ```