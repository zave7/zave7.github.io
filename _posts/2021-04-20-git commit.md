---
title: git commit
categories: Git
---

# $ git commit - Record changes to the repository
- `git commit`
    - index 영역의 내용을 기반으로 커밋 오브젝트를 생성하는 명령이다.
    - 커밋 오브젝트에는 부모 커밋의 해시 값과, root tree 해시 값에 대한 정보가 들어있다.

git commit
- 커밋과 동시에 커밋 메세지를 입력하는 명령어  

git commit -v
- 커밋하는 변경사항을 한번 더 보여준다
- 커밋 메세지를 입력하는 화면 아래 코드 diff

git commit -a
- 스테이징된 모든 파일을 커밋

git commit -m "comment"
- 커밋 메세지를 인라인에서 작성

git commit --amend
- 가장 최근 커밋을 수정
- 커밋 해시값이 달라진다.