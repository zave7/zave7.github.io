---
title: JUnit5 Annotation
categories: junit
---

# 어노테이션 정리

## 1. Method or Class
### @DisplayName
  - 사용자 지정 표시 이름을 선언한다.
  ***
## 2. Method
### @Test
- 테스트 메서드임을 나타낸다.
### @ParameterizedTest
  - 매개변수화 된 테스트 메서드임을 나타낸다.
### @RepeatedTest
  - 반복 테스트를 위한 테스트 템플릿 메서드임을 나타낸다.
### @TestFactory
  - 동적 테스트를 위한 테스트 팩토리 메서드임을 나타낸다.
### @TestTemplate
  - 등록된 공급자가 반환한 호출 컨텍스트의 수에 따라 여러번 호출되도록 설계된 테스트 케이스의 템플릿 메서드임을 나타낸다.
  ***
## 3. Class
### @TestMethodOrder
  - 어노테이션이 선언된 테스트 클래스에 대한 테스트 메서드 실행 순서를 구성하는데 사용되며, JUnit 4의 `@FixMethodOrder`와 유사하다.
### @TestInstance
  - 어노테이션이 선언된 테스트 클래스에 대한 테스트 인스턴스 수명 주기를 구성하는데 사용된다.
### @DisplayNameGeneration
  - 테스트 클래스에 대한 사용자 지정 표시 이름 생성기를 선언한다.