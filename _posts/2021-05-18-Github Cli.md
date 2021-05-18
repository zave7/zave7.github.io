---
title: 깃허브 CLI 
categories: Github
---

# Github CLI 소개

### 1. 설치  
- [Github CLI](https://cli.github.com/) 홈페이지 접속 후 다운로드

### 2. could not prompt 에러 발생 시
- `2.31.1` 버전 이상으로 깃을 업데이트 
- 설치 과정중 맨 마지막 옵션 체크
    ![setup](/images/github/cli/error/setup.PNG)

### 3. pr 생성
- `gh pr create --base develop --repo [HOST]/origin/app --head my:feature`
    - --base : pr을 요청할 저장소의 브랜치를 지정하는 옵션
    - --repo : pr을 요청할 저장소를 지정하는 옵션 (host는 옵션이다)
    - --head : fork 한 자신의 저장소의 브랜치 지정