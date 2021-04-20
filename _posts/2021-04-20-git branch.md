---
title: git branch
categories: Git
---

# $ git branch
- `git branch`
    - 현재 로컬의 브랜치 리스트를 조회하는 명령이다.
    - 브랜치의 상세한 개념은 추후 내용을 채워넣겠다..

git branch
- 로컬 브랜치의 목록 확인

git branch -v(--verbose)
- 브랜치의 간단한 내용까지 조회

git branch [branch-name]
- 로컬 브랜치 생성

git branch -d(--delete) [branch-name]
- 병합이 완료된 브랜치 삭제

git branch -D [branch-name]
- 병합하지 않은 브랜치를 강제 삭제

git branch -a 
- 현재 생성된 모든 local branch와 remote branch 확인

git branch --set-upstream-to origin/feature-01
- branch 연동