---
title: git area, objects
categories: Git
---

## # **Area**

- **Working Directory**
    - 실제 프로젝트 디렉토리, git 이력과 관련된 정보가
    저장되어있는 .git 디렉토리를 제외한 모든 영역
    - 실제 코드를 수정하고 추가하는 변경이 이루어지는 디렉토리
- **Index**
    - Working Directory 에서 Repository로 정보가 저장되기 전
    준비 영역
    - .git/index 파일로 관리됨.
- **Repository**
    - 파일이나 tree를 변경 이력별로 저장해 두는 곳
    .git 디렉토리 내에 존재함
    - Local Repository : 내 PC에 파일이 저장되는 개인 저장소
    - Remote Repository : 파일이 원격 저장소 전용 서버에서
    관리되며 여러 사람이 함께 공유하기 위한 저장소
- **Stash**
    - 일반적인 Working Directory > Index > Repository 로 이루
    어지는 영역과는 다른 별개의 임시영역
    - 임시적으로 작업사항을 저장해놓고 나중에 꺼내올 수 있다.

## # **Object**

- git은 3가지 타입의 오브젝트로 버전관리를 한다.
    - 100644(일반 파일), 100755(실행 파일), 040000(디렉토리)
    - 아래 커맨드로 각각의 오브젝트의 타입과 내용을 확인할 수 있다.
        - git cat-file -t [해시값]
            
            - 타입 조회
            
        - git cat-file -p [해시값]
            
            - 내용 조회
            
- **type**

    ---
    - <span style="color:green"><b>blob</b></span>
        - 파일명 같은 메타데이터 없이, 바이너리 데이터 자체만 zlib 압축 라이브러리로 압축하여 저장
        - '\0' 는 헤더의 끝을 나타냄
            <aside>
            💡 < 저장 형식 ><br/>
            Header : blob_{byteSize}\0<br/>
            Body :<br/>
            </aside>
    ---
    - <span style="color:blue"><b>tree</b></span>
        - blob 와 tree 의 정보를 갖는다.
            <aside>
            💡 < 저장 형식 ><br/>
            100644(타입) blob a5bce3f...c6f42d0504a848bd5 test1.txt<br/>
            100644(타입) blob 8a8363...d181321626be514c7f4 test2.txt<br/>
            040000(타입) tree 8a8363...ed61321626be514c7f4 etc<br/>
            </aside>
    ---
    - <span style="color:orange"><b>commit</b></span>
        - 구성 요소 : root tree, parent commit, author, committer
        - 일반 커밋과 merge 커밋으로 나뉜다.
            <aside>
            💡 < 일반 commit ><br/>
            tree d537288f8e58761133a9367be3477d79365b2b29<br/>
            parent db74711b3f977ddaed5bd01cbf8f78663e3f1721<br/>
            author zave7 <zave7@naver.com> 1634614163 +0900<br/>
            committer zave7 <zave7@naver.com> 1634614163 +0900<br/>
            </aside>
        - merge 커밋은 2개의 부모 커밋을 갖는다.
            <aside>
            💡 < merge commit ><br/>
            tree c506115755a3eaac4043bee111f07e351e3d4ad5<br/>
            parent c36876f07e29572ea9a1f22a4c7e43ca62173a72<br/>
            parent 11a227f98d37ce9939c2c5ce8bab378bef688a9f<br/>
            author zave7 <zave7@naver.com> 1634614291 +0900<br/>
            committer zave7 <zave7@naver.com> 1634614291 +0900<br/>
            </aside>
    
- **hash**
    - 깃은 파일을 SHA-1로 해시하여 해시값은 key 로, 압축된 파일은 value 로 key-value 형식으로 관리한다.
    - 해시값 40자 중 앞의 2자리는 디렉토리명으로 사용하고 나머지 38자는 오브젝트 파일의 실제 파일명으로 사용된다.
    - 메타데이터를 포함하지 않고 해시하기 때문에 파일명이 다르지만 내용이 같은 파일을 여러개 저장할 경우 하나의 blob로만 관리된다. 
    (tree 에서 여러 파일명들이 같은 blob 를 바라보고 있음)

## # **3 way merge**

- git 은  브랜치의 머지가 일어날때 우선적으로 3 way merge 를 시도하고 병합이 불가능할 경우 사용자에게 conflict 를 해결하도록 안내한다.
- base branch를 기준으로 merge 의 대상 브랜치와 비교하여 마지막에 변경된 부분을 반영한다.
- 각 브랜치가 모두 변경한 부분이 있을 경우 conflict 발생한다.

![Untitled](/images/git/3waymerge.png)

### # .git 내부

- /object : 모든 오브젝트가 저장되는 디렉토리
    - /2자/38자
- index : stage 에 있는 파일들의 상태가 저장되는 파일
    - index 와 마지막 커밋을 비교하여 커밋할 파일이 있는지 판단한다.
    - index 와 working directory 의 파일들을 피교하여 수정된 파일을 확인한다.
- /refs : 브랜치와 태그가 저장되는 디렉토리
    - /heads/branchfiles.. : 생성된 브랜치명으로 파일명이 정해지고 각 파일에는 브랜치가 가리키고 있는 commit object 아이디가 저장된다.
- /hooks : 깃에서 지원하는 기본적인 hook script 파일들이 있는 디렉토리
    - 클라이언트 훅
        - pre-commit : 커밋 메세지를 작성하기 전에 호출
        - post-commit : 커밋이 완료되면 실행
        - pre-rebase : rebase 하기 전에 실행
        - post-merge : merge 가 완료되면 실행
        - pre-push : remote 로 데이터를 전송하기 전에 실행
        - pre-auto-gc : git 은 가끔씩 git gc —auto 명령으로 가비지 컬렉션을 동작시키는데 동작전에 호출된다.
    - 서버 훅
        - pre-receive : remote 서버의 bare repository 에서 실행되는 hook
        한번에 브랜치를 여러개 push 하더라도 한번만 실행된다.
        push 정책을 설정할 수 있다.
        - update : pre-receive 와 거의 비슷하지만 각 브랜치마다 실행된다.
        - post-receive : push 한 후에 실행된다.
- /logs : 실행된 모든 커맨드에 대한 로그가 저장되는 디렉토리
    - HEAD : HEAD 즉 모든 로그가 저장되는 파일
    - /refs/heads/files.. : 각 브랜치마다 로그가 분리되어 저장된다.