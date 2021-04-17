---
title: No property [methodName] found for type [Entity]! 익셉션 발생
categories: Querydsl
---

## - 문제
  - 커스텀 인터페이스와 구현체를 작성하여 애플리케이션 실행 시 `No property [methodName] found for type [Entity]!` 가 발생했다.
## - 원인
  - 스프링이 repository 구현체를 naming 규칙에 따라 생성하는데 그 규칙이 '커스텀인터페이스명 + Impl' 이다. 
  - 그렇기 때문에 구현체 이름의 인터페이스의 이름을 따라가지 않으면 구현체가 생성되지 않는다.
  - 따라서 스프링은 Spring Data Jpa method 네이밍 규칙에 존재하지 않는 메서드를 구현체에서 찾지 못하고 최종적으로 Entity의 property 에서 찾으려 했으나 당연히 없으므로 익셉션이 발생했다.
## 해결
  - 구현체 클래스 이름을 naming 규칙에 맞춰 변경했다.