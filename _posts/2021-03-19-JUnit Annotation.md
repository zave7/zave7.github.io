---
title: JUnit5 Annotation
categories: junit
---

# 어노테이션 정리

## 1. Method or Class
### @DisplayName
  - 사용자 지정 표시 이름을 선언한다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-display-names)]
### @Tag
  - 클래스 또는 메서드 수준에서 [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-tagging-and-filtering)]를 선언하는 데 사용된다.
### @Disabled
  - 테스트 클래스 또는 테스트 메서드를 비활성화 하는데 사용된다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-disabling)]
  - JUnit4의 `@Ignore`와 유사하다.
  ***
## 2. Method
### @Test
- 테스트 메서드임을 나타낸다. [[Reference document 링크]()]
### @ParameterizedTest 
  - 매개변수화 된 테스트 메서드임을 나타낸다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests)]
### @RepeatedTest
  - 반복 테스트를 위한 테스트 템플릿 메서드임을 나타낸다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-repeated-tests)]
### @TestFactory
  - 동적 테스트를 위한 테스트 팩토리 메서드임을 나타낸다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-dynamic-tests)]
### @TestTemplate
  - 등록된 공급자가 반환한 호출 컨텍스트의 수에 따라 여러번 호출되도록 설계된 테스트 케이스의 템플릿 메서드임을 나타낸다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#extensions-test-templates)]
### @BeforeEach
  - 클래스의 각 `@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory`가 선언된 메서드 이전에 실행되는 메서드임을 나타낸다. JUnit 4의 `@Before`와 유사하다. 
### @AfterEach
  - 클래스의 각 `@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory`가 선언된 메서드 이후에 실행되는 메서드임을 나타낸다. JUnit 4의 `@After`와 유사하다. 
### @BeforeAll
  - 클래스의 각 `@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory`가 선언된 메서드 이전에 딱 한번만 실행되는 메서드임을 나타낸다. 해당 메서드는 static 으로 작성되어야 한다.JUnit 4의 `@BeforeClass`와 유사하다. 
### @AfterAll
  - 클래스의 각 `@Test`, `@RepeatedTest`, `@ParameterizedTest`, `@TestFactory`가 선언된 메서드 이후에 딱 한번만 실행되는 메서드임을 나타낸다. 해당 메서드는 static 으로 작성되어야 한다.JUnit 4의 `@AfterClass`와 유사하다. 
### @Timeout
  - test, test factory, test template, lifecycle 메서드가 주어진 실행 시간을 초과할 경우 실패한다. [[Reference document 링크]()]
### @TempDir
  - lifecycle 또는 test 메서드에서 필드 주입 또는 매개 변수 주입을 통해 임시 디렉토리를 제공하는데 사용된다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-built-in-extensions-TempDirectory)]
  ***
## 3. Class
### @TestMethodOrder
  - 어노테이션이 선언된 테스트 클래스에 대한 테스트 메서드 실행 순서를 구성하는데 사용되며, JUnit 4의 `@FixMethodOrder`와 유사하다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-test-execution-order)]
### @TestInstance
  - 어노테이션이 선언된 테스트 클래스에 대한 테스트 인스턴스 수명 주기를 구성하는데 사용된다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle)]
### @DisplayNameGeneration
  - 테스트 클래스에 대한 사용자 지정 표시 이름 생성기를 선언한다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#writing-tests-display-name-generator)]
### @Nested
  - 해당 어노테이션이 선언된 클래스는 중첩된 비정적(non-static) 테스트 클래스 임을 나타낸다. [[Reference document 링크]()]
  - `@BeforeAll` 및 `@AfterAll` 메서드는 "per-class" [테스트 인스턴스 라이프사이클](https://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle)을 사용하지 않는 한 `@Nested` 테스트 클래스에서 직접 사용할 수 없다.
  - 테스트 클래스 안에서 내부(Inner Class)를 정의해 테스트를 계층화할 수 있다.
  - 내부 클래스로 정의하기 때문에 부모 클래스의 멤버 필드에 접근할 수 있고, `@Before`, `@After` 와 같은 테스트 생명주기에 관계된 메서드들도 계층에 맞게 동작한다.
### @ExtendWith
  - 확장을 선언적으로 등록할 때 사용된다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#extensions-registration-declarative)]
## 4. Field
### @RegisterExtension
  - 필드를 통해 프로그래밍 방식으로 확장을 등록할 때 사용된다. [[Reference document 링크](https://junit.org/junit5/docs/current/user-guide/#extensions-registration-programmatic)]