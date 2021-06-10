---
title: git submodule
categories: Git
---

# $ git submodule - Initialize, update or inspect submodules
- `git submodule`
    - 하위 모듈을 상위 모듈과 함께 버전관리를 할 수 있도록 하는 명령이다.
    - 기본적으로 최상위 디렉토리 하위에 서브모듈의 디렉토리가 존재한다.(경로 지정도 가능)
    - .gitmodules 파일에 서브 모듈에 대한 메타데이터가 존재한다.

### 1. 서브 모듈 추가
1. 하위 모듈로 추가하고 싶은 저장소를 add 명령으로 추가한다.
    ```
    git submodule add [repository] [path]
    ```
    - repository : git 저장소 URL (필수)
    - path : 서브 모듈이 관리될 디렉토리 경로를 지정할 수 있다.(옵션)
2. 단계별 실행 내용
    - repository 생성

        ![init](/images/git/submodule/init.png)

    - 빈 커밋 생성

        ![init-commit](/images/git/submodule/init-commit.png)

    - 서브 모듈 추가

        ![add-submodule](/images/git/submodule/add-submodule.png)

    - 메인 저장소의 상태 확인 후 커밋
        1. .gitmodules 파일과 submodule 파일이 생성되었음을 확인

            ![check-submodule](/images/git/submodule/check-submodule.png)

        2. .gitmodules 내용

            ![gitmodules](/images/git/submodule/gitmodules.png)

        3. ls

            ![dir-submodule](/images/git/submodule/dir-submodule.png)

        4. commit

            ![commit-sub](/images/git/submodule/commit-submodule.png)

        5. log

            ![log-sub](/images/git/submodule/log-submodule.png)

    - 서브 모듈의 커밋 히스토리 확인

        - 가장 최근 커밋 아이디 `c25acfbc10f86c01114297e64b631fd0c23a7240`

            ![sub-history](/images/git/submodule/sub-history.png)
    
    - 메인 저장소 커밋에서 가리키고 있는 서브모듈의 커밋 아이디 확인

        1. 메인 저장소의 root tree 해시값 확인 `e77280e67b117b46397d4dca817186aa274e45c0`

            ![commit-tree](/images/git/submodule/commit-tree.png)
        
        2. root tree 정보에 서브 모듈을 추가한 시점의 가장 최근 커밋 아이디가 포함되어있는 것을 확인할 수 있다.

            ![sub-commit](/images/git/submodule/sub-commit.png)