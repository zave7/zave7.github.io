---
title: "Docker Spring Profile 적용"
categories: Docker
---

# 도커 컨테이너 실행 시 스프링부트 profile 적용

1. dockerfile에 ENTRYPOINT 설정
```
ENTRYPOINT ["java","-jar","/home/app/deploy/server.jar"]
```
2. 컨테이너 run 시 환경변수 지정
```
docker run -e "SPRING_PROFILES_ACTIVE=test" --name con test
```
