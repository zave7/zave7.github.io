---
title: JUnit UnnecessaryStubbingException 발생
categories: JUnit
---

# 1. 문제
1. JUnit(Jupiter) Mockito 클래스의 `when`, `thenReturn` 을 이용하여 테스트 코드 작성
2. 테스트 코드 실행 시 아래 익셉션 발생!
    ```java
    org.mockito.exceptions.misusing.UnnecessaryStubbingException: 
    Unnecessary stubbings detected.
    Clean & maintainable test code requires zero unnecessary code.
    Following stubbings are unnecessary (click to navigate to relevant line of code):
        1. -> at com.test.junit.statistic.service.StatisticServiceTest.getDataListTest(StatisticServiceTest.java:63)
    Please remove unnecessary stubbings or use 'lenient' strictness. More info: javadoc for UnnecessaryStubbingException class.
    ```

# 2. 원인
1. 테스트 실행 중 스텁 메서드로 작성한 부분이 실제 로직에서 호출되지 않는 것을 JUnit 이 감지
2. 익셉션 내용에 써있는 것처럼 불필요한 스텁 메서드 작성은 테스트 코드 유지보수에 도움이 되지 않으므로 `UnnecessaryStubbingException` 익셉션을 발생시킨다.

# 3. 해결
1. `Mockito` 클래스의 static method 인 `lenient()` 를 사용하여 해당 제약을 느슨하게 해주면 된다.
    ```java
    lenient().when(userRepository.findById(any())).thenReturn(getUser());
    ```

# 4. 여담
- 일단은 `lenient()` 를 사용해서 처리해놓긴 했지만 실제 테스트 되지 않는 부분을 스터빙 해놓았다는 것은 테스트 코드가 잘못 작성되어있다고 생각된다.
- 로직의 모든 부분을 테스트할 수 있도록 작성하거나 테스트 코드에 충분한 테스트 데이터를 넣어야 할것같다!