---
title: "JUnit"
categories: JUnit
---

# JUit

## JUnit 핵심 객체
  - Assert : 테스트하려는 조건을 명시한다. assert 메서드는 조건이 만족되면 아무 일도 없었다는 듯이 조용히 지나가며, 만족되지 못하면 예외를 던진다.
  - Test : @Test 어노테이션이 부여된 메서드로, 하나의 테스트를 뜻한다. JUnit은 먼저 메서드를 포함하는 클래스의 인스턴스를 만들고, 어노테이션된 메서드를 찾아 호출한다.
  - Test 클래스 : @Test 메서드를 포함한 클래스이다.
  - Suite : 스위트는 여러 테스트 클래스를 하나로 묶는 수단을 제공한다.
  - Runner : 러너는 테스트를 실행시킨다. JUnit 4는 하위 호환성을 유지하여, JUnit 3의 테스트도 역시 실행할 수 있다.
  
### 파라미터화 테스트
```
@RunWith(value= Parameterized.class)
public class ParameterizedTest {

    private double excepted;
    private double valueOne;
    private double valueTwo;

    @Parameterized.Parameters
    public static Collection<Integer[]> getTestParameters() {
        return Arrays.asList(new Integer[][]{
                {2, 1, 1},
                {3, 2, 4}
        });
    }
    public ParameterizedTest(double expected, double valueOne, double valueTwo){
        this.excepted = expected;
        this.valueOne = valueOne;
        this.valueTwo = valueTwo;
    }

    @Test
    public void sum() {
        Calculator calculator = new Calculator();
        assertEquals(excepted, calculator.add(valueOne, valueTwo), 0);
    }
}
```
  1. 테스트 클래스에는 반드시 @RunWith 어노테이션을 부여해야하며, 그 파라미터로는 Parameterized 클래스를 사용한다.
  2. 테스트에 사용될 값을 인스턴스 변수로 선언하고
  3. @Parameters 라 표시도니 메서드가 하나 필요하다.
  4. 위 예제에서는 getTestParameters 메서드가 여기에 해당된다. 이 메서드의 시그니쳐는 반드시 @Parameters public staic java.util.Collection 이어야 하며,
    어떠한 파라미터도 입력 받아서는 안된다. 컬렉션의 원소는 배열리고, 길이는 모두 같아야 한다. 또한 그 길이는 유일한 public 생성자가 받는 세 개의 파라미터를 받으므로 
    각 배열의 원소도 세 개이다.
  - 테스트의 반복 횟수는 @Parameters 메서드가 반호나하는 컬렉션의 크기에 의해 결정된다. 즉 이 테스트 케이스를 한번만 실행하면, 아래처럼 매번 다른 값으로 sum 메서드를 세번 호출한 것과 동일한
    효과를 갖는다.
