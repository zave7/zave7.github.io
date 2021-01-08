# 리눅스 명령어

## - find *찾기*
- 특정 이름의 디렉토리 찾기
  $ find . -type d -name "test"
- 생성된지 5일이 지난 디렉토리 찾기
  $ find . -type d -mtime +5
- 현재 디렉토리에서 바로 하위 디렉토리만 찾기 (. 제외)
  $ find `pwd` -maxdepth 1 ! -path `pwd` -type d
  $ find `pwd` -maxdepth 1 ! -path `pwd` -type d

## wc *사용자가 지정한 파일의 행, 단어, 문자수를 세는 프로그램*
- 파일의 문자 갯수 세기
  $ wc -c test.txt
- 파일의 단어 갯수 세기
  $ wc -w
- 파일의 행 라인 세기
  $ wc -l
- ls와 같은 명령어의 결과를 파이프를 통해 wc입력
  $ ls -al | wc -l
