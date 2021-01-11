# Linux Crontab

### # cron 표현식

  - 1분 마다 실행
  ```
  * * * * * test.sh
  ```
  - 동일 프로세스를 10분 마다 실행
  ```
  */10 * * * * test.sh
  ```
  - 매시 15분 마다 실행
  ```
  15 * * * * test.sh
  ```
  - 1시간 마다 실행
  ```
  0 * * * * test.sh
  ```
  - 2시간 마다 실행
  ```
  0 */2 * * * test.sh
  ```
  


### # crontab 명령어
  - 명령을 등록, 편집 ( 맨 처음 사용시 편집기 선택 )
  ```
  $ crontab -e
  ```
  - 등록된 명령을 삭제
  ```
  $ crontab -d
  ```
  - 현재 등록된 리스트 출력
  ```
  $ crontab -l
  ```
  - testuser 사용자가 등록한 crontab 리스트 출력
  ```
  $ crontab -l -u testuser
  ```
  - 현재 사용자가 등록한 crontab 전체 삭제
  ```
  $ crontab -r
  ```
