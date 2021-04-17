---
title: "Window vim"
categories: Win-Tool
---

# PowerShell vim 설치

## Choco
  - vim 을 설치하려면 우선 패키지 매니저를 설치해야한다.
  - Get-Package 존재하긴 하지만 사용이 불편하기 때문에 Chocolatey 라는 윈도우 패키니 매니저를 설치한다.
  
### Choco 설치 방법
  - 아래 코드를 powershell에 복붙해서 실행하면 설치된다.
  ```
  Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
  ```

### vim 설치
  - console 용 vim 설치:
  ```
  choco install vim-console -y
  ```
  - GUI 버전도 함께 설치:
  ```
  choco install vim -y
  ```
