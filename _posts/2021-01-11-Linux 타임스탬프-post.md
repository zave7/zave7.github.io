# Linux 타임 스탬프

## 타임 스탬프 종류
  1. atime 
    - <b>Last Access Time</b> : 마지막으로 접근한 시간
  2. mtime
    - <b>Last Modification Time</b> : 마지막으로 수정한 시간
  3. ctime
    - <b>Last Change Time</b> : 속성을 마지막으로 수정한 시간
   
### # File
  - atime : 
    - touch
    - 조회
    - 내용 수정(저장)
  - mtime : 
    - touch
    - 내용 수정(저장)
  - ctime : 
    - touch
    - 내용 수정(저장)
    - 이름 변경
    - 권한 변경
    - 소유자 변경
    - 기타 모든 메타데이터의 변경
  - ※ 내용을 변경하지 않고 w로 저장하는 행위 자체도 inode 값이 변경된다. 따라서 mtime과 ctime에 영향을 미친다.
### # Directory
  - atime : touch, 디렉토리 생성
  - mtime : 
    - touch
    - 하위 디렉토리 [생성, 이름 변경, 삭제]
    - 하위 파일 [생성, 수정(저장), 삭제, 이름 변경] 
  - ctime : 
    - touch
    - 이름 변경
    - 권한 변경
    - 소유자 변경
    - 기타 모든 메타데이터의 변경
