---
title: 도커 로그
categories: docker
---
# - Docker Log
- 별다른 설정을 하지 않았을 경우 컨테이너의 표준 출력 로그 아래와 같은 경로에 쌓이게 된다
    - /var/lib/docker/containers/<cotainer-id>/<container-id>-json.log
- log 가 계속 쌓여서 disk full 이 발생할 수도 있으니 디스크 용량이 얼마 없을 경우 확인해보는게 좋다
- 특정 컨테이너 로그 삭제
    ```
    $ sudo truncate -s 0 /var/lib/docker/containers/<cotainer-id>/<container-id>-json.log
    ```
- logrotate 를 이용한 로그 로테이터 설정
    ```
    $ vi /etc/logrotate.d/docker
    ```
    ```
    /var/lib/docker/containers/*/*.log {
        rotate 7
        daily
        compress
        missingok
        copytruncate
    }
    ```
    - 리눅스 loglrotate 작성 방법
        - rotate : 최대 파일 보관 갯수 (ex. log.1, log.3, log.2 ...)
        - daily : 로그 회전 주기 (yearly=매년, monthly=매월, weekly=매주, daily=매일)
        - compress : 로그 파일 압축
        - size=1M : 크기가 1메가 바이트를 넘으면 실행
        - missingok : 각 로테이션에 해당하는 로그 파일이 없을 경우 에러메세지를 출력하고 다음으로 실행
        - copyturncate : 복사본을 만들고 크기를 0으로 설정
    - 바로 실행
        ```
        $ sudo logrotate -fv /etc/logrotate.d/docker
        ```