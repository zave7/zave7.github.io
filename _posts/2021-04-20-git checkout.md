---
title: git checkout
categories: Git
---

# $ git checkout - Switch branches or restore working tree files
- `git checkout`
    - 특정 커밋의 상태로 전환하는 명령이다.
    - 체크아웃의 상세한 내용은 추후 채워넣겠다..

### $ git checkout branch-name
- 해당 브랜치로 전환

### $ git checkout -b branch-name
- 브랜치를 생성하고 전환까지

### $ git checkout --[Filename]
- 스테이징에 커밋하지 않은 파일의 변경 내용을 취소하고 이전 상태로 되돌린다

### $ git checkout .
- working directory에서 수정한 파일(git add이전)을 현재 버전으로 되돌리기

### $ git checkout -f 
- 아직 커밋되지 않은 working directory 와 index(staging area) 수정사항 모두 삭제