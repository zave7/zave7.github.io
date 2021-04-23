---
title: git remote
categories: Git
---

# $ git remote - Manage set of tracked repositories
- `git remote`
    - 원격 저장소를 지정하거나 조회할때 사용하는 명령이다.
    - 여러 저장소를 지정할 수 있다.

### $ git remote add [remote-name] [원격저장소주소]
- 원격저장소의 별칭을 `[remote-name]` 로 지정하며 추가

### $ git remote
- 현재 원격저장소로 설정된 목록 확인

### $ git remote -v(--verbose)
- 현재 원격저장소로 설정된 목록 확인 (URL 포함)

### $ git remote show [remote-name]
- 리모트 저장소의 구체적인 정보를 확인
- 브랜치명을 생략하고 git push 명령을 실행 할 때 어떤 브랜치가 어떤 브랜치로 push 되는지도 보여준다

### $ git remote rename test1 test2
- 리모트 이름을 test1 에서 test2 로 변경

### $ git remote rm origin
- origin 리모트 저장소 삭제