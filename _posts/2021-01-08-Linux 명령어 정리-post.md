---
title: "Linux Command"
categories: Linux
---

# 리눅스 명령어

## - find *찾기*
- 특정 이름의 디렉토리 찾기
  ```
  $ find . -type d -name "test"
  ```
- 생성된지 5일이 지난 디렉토리 찾기
  ```
  $ find . -type d -mtime +5
  ```
- 현재 디렉토리에서 바로 하위 디렉토리만 찾기 (. 제외)
  ```
  $ find `pwd` -maxdepth 1 ! -path `pwd` -type d
  ```

## - wc *사용자가 지정한 파일의 행, 단어, 문자수를 세는 프로그램*
- 파일의 문자 갯수 세기
  ```
  $ wc -c test.txt
  ```
- 파일의 단어 갯수 세기
  ```
  $ wc -w
  ```
- 파일의 행 라인 세기
  ```
  $ wc -l
  ```
- ls와 같은 명령어의 결과를 파이프를 통해 wc입력
  ```
  $ ls -al | wc -l
  ```

## - stat *파일이나 디렉토리의 시각 정보 조회*
- 파일의 시각 정보 조회
  ```
  $ stat test.txt
  ```
- 디렉토리의 시각 정보 조회
  ```
  $ stat ./test/
  ```
  
## - grep *문자열 검색*
  - 입력으로 전달된 파일의 내용에서 특정 문자열을 찾고자할 때 사용하는 명령어
    ### -r *하위 디렉토리 검색*
      - 현재 폴더의 log 파일에서 "test" 검색
        ```
        $ grep -r "test" ./*.log
        ```
    ### -o *매치되는 문자열만 표시*
      - 특정 파일에서 test 검색
        ```
        $ grep -o test *.log
        ```

## - more *파일 내용 확인*
  1. 화면 단위로 끊어서 출력하는 명령어이다. 위에서 아래 방향으로만 출력 되기 때문에, 지나간 내용을 다시 볼 수 없는 단점이있다.
  2. 화면 왼쪽 하단에 출력된 내용이 전체의 몇 퍼센트인지를 표시하며, Enter 키를 입력하면 한 줄씩 출력되고, space bar 를 입력하면 한 화면씩 출력된다. 
  - 파일의 내용을 확인
    ```
    $ more file.txt
    ```
  
## - 메모리 사용량 순 프로세스 보기
  1. RSS(Resident set size) : 물리 메모리를 실제 점유하고 있는 크기
  - 간단히 보기
    ```
    $ ps -ef --sort -rss
    ```
  - 상위 10개
    ```
    ps -ef --sort -rss | head -n 11
    ```
  - 메모리 사용량 표시 (Kb)
    ```
    $ ps -eo user,pid,ppid,rss,size,vsize,pmem,pcpu,time,cmd --sort -rss | head -n 11
    ```
  - 명령 인수 숨기기 ( cmd -> comm )
    ```
    $ ps -eo user,pid,ppid,rss,size,vsize,pmem,pcpu,time,comm --sort -rss | head -n 11
    ```

## - 디렉토리 용량 확인
  1. 용량 단위 (KByte)
  - 특정 디렉토리 및 하위 디렉토리 용량 확인
    ```
    $ du .
    $ du ./test/
    ```
  - 특정 디렉토리 용량만 확인
    ```
    $ du -s .
    $ du -s ./test/
    # 용량 조회 편하게
    $ du -sh .
    $ du -sh ./test/
    ```
  
  
