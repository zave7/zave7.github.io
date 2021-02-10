---
title: "AWS RDS 설정"
categories: AWS
---

## 문제
  - RDS mariaDB에 Trigger를 생성이 되지 않는다.
  
## 원인
  - AWS RDS는 SYS 엑세스(SUPER 권한)를 제공하지 않는다.
  
## 해결방법
  - MySQL DB 인스턴스에서 바이너리 로깅을 활성화한 경우 DB 인스턴스에 대해 생성하는 사용자 지정 DB 파라미터 그룹에서 log_bin_trust_function_creators 파라미터를 true로 설정합니다. 자세한 내용은 Amazon RDS의 마스터 사용자 계정 권한을 참조하면된다.
