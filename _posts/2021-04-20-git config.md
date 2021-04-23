---
title: git config
categories: Git
---

# $ git config - Get and set repository or global options
- 깃의 환경설정 명령어이다.
- 환경설정을 잘 활용하면 효율적으로 깃을 사용할 수 있게된다.
- 설정은 key=value 형식으로 이루어지는데, Git은 여파 설정 파일을 참조하므로 키가 중복으로 존재할 수 있다. 이 때 Git 나중의 값을 우선으로 사용한다.

### $ git config [--global] user.name "name"
- 작업자의 이름을  설정하는 옵션이다. 필수적으로 설정해야한다.
- `user.name` 이라는 키에 `name` 이라는 값을 매핑
### $ git config [--global] user.email "email@email.com"
- 작업자의 이메일을 설정하는 옵션이다. 필수적으로 설정해야한다.
- 잘못 적으면 git hub의 커밋 잔디가 심어지지 않는다.
- `user.email` 이라는 키에 `email@email.com` 이라는 값을 매핑

### $ git config --list
- 모든 설정 값을 보여준다.

### $ git config --global gui.encoding utf-8
- 화면에서 한글이 깨질 경우 인코딩 방식을 설정해주면 된다.

### $ git config --global alias.cb "checkout -b"
- 깃 커맨드도 다른 시스템과 마찬가지로 alias 설정이 가능하다.
- `checkout -b` 명령을 `cb` 로 간단하게 매핑