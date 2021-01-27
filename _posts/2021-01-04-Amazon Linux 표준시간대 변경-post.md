---
title: "AWS EC2 표준 시간대 변경"
categories: AWS
---

# Amazon Linux에서 표준 시간대 변경

1. 인스턴스에서 사용할 표준 시간대 식별 (/usr/share/zoneinfo)
  - 한국 : /usr/share/zoneinfo/Asia/Seoul
2. /etc/sysconfig/clock 팡리을 새 표준 시간대로 업데이트
  ```
  $ sudo vi /etc/sysconfig/clock
  -
  ZONE="Asia/Seoul"
  ```
  - UTC=true 는 변경하지 않는다 ( 이 항목은 하드웨어 클록에 관한 것으로, 인스턴스에 대해 다른 표준 시간대를 설정할 때 따로 조정할 필요가 없다 )
  
3. 인스턴스가 현지 시간 정보를 참조할 때 표준 시간대 파일을 찾을 수 있도록 /etc/localtime 과 표준 시간대 파일 사이에 심볼 링크를 생성
  ```
  $ sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime
  ```
4. 시스템을 재부팅 하여 모든 서비스와 애플리케이션에 새로운 표준 시간대 정보를 적용
  ```
  $ sudo reboot
  ```
5. 표준 시간대 업데이트 확인
  ```
  $ date
  ```
