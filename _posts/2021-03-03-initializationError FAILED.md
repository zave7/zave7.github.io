---
title: initializationError FAILED
categories: springboot
---

# 스프링부트 initializationError FAILED

## 문제
  - jar build 시 initializationError FAILED 에러가 발생하면서 실패했다.

## 원인
  - 구글링 결과 대부분 junit 라이브러리가 추가되지 않아서 발생한다고 했지만 그것과는 관련이 없다.
  - 스프링부트는 기본적으로 junit 라이브러리를 포함하고 있기 때문이다.
  - 직감으로 단번에 ApplicationTests 클래스가 있는 패키지 경로가 올바르지 않아서 발생하는것을 찾아냈다.

## 해결
  - Application 클래스와 패키지 경로를 동일하게 맞춰서 해결했다.
