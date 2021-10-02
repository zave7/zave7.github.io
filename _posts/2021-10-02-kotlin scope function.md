---
title: kotlin scope function
categories: Kotlin
---

# 코틀린 스코프 함수
- 코틀린 표준 라이브러리는 객체의 컨텍스트 내에서 코드 블럭을 실행하기 위한 목적만을 가진 여러가지 함수를 제공한다.
- 이런 함수들을 람다식으로 호출할 때, 이는 임시로 범위(scope) 를 형성한다.
- 이 범위 내에서는 객체의 이름이 없어도 객체에 접근 할 수 있다. 이러한 함수를 `scope function` 이라고 한다.
- 종류
    - run
    - let
    - apply
    - also
    - with
- 차이점
    - scope 함수는 본질이 비슷하지만 각 scope 함수에는 두 가지 큰 차이점이 있다.
        - 객체의 컨텍스트를 참조하는 방식
        - 리턴 값 (this or it)
  
---
## 1. <b>run</b>
- 객체의 컨텍스트를 참조하는 방식
    - 람다 수신자로써의 컨텍스트를 this 키워드로 참조한다.
    - `run` 을 사용할 경우 내부 scope 는 this 의 성질을 같는다.
- 리턴 값
    - 함수 리터럴의 마지막 expression
- 비확장 함수로도 사용가능
    - 표현식이 필요한 곳에서 다수의 구문 블럭을 실행할 수 있도록 해준다.
- case
    - 객체 초기화와 결과를 계산할 때
    - expression 이 필요한 곳에 statements 을 실행할 때
- code
    ```kotlin
    class RunScope(val name: String, val age: Int)

    fun main() {

        val run = RunScope("testRun", 3)
        val plusFive = run.run {
            println("객체 컨텍스트 내의 run 실행")
            this.age + 5
            // or age + 5
        }
        println(">>> 컨텍스트 내 실행 결과 : $plusFive")

        // 비확장 함수로 사용
        val run1 = run {
            println("비확장 함수 실행")
            1 + 10
        }
        println(">>> 비확장 함수 실행 결과 : $run1")

    }
    ```
  
---
## 2. <b>let</b>
- 객체의 컨텍스트를 참조하는 방식
    - 컨텍스트 객체를 람자 인자로 가진다.
    - 암시적인 기본 이름인 it 으로 접근이 가능하다.
- 리턴 값
    - 함수 리터럴의 마지막 expession ( scope 의 마지막 값을 리턴)
- case
    - null 이 아닌 객체에 람다를 실행할 때
    - 지역 scope 에서 expression을 변수로 선언할 때
- code
    ```kotlin
    class LetScope(val name: String, val age: Int?) {

        override fun toString(): String {
            return "LetScope(name='$name', age=$age)"
        }
    }

    // top-level function
    fun isOdd(let: LetScope) : Boolean {
        if(let.age != null) {
            return let.age % 2 == 1
        }
        return false
    }

    fun main() {

        // 1. 기본 let
        val let = LetScope("letScope", 7)
        val minusSix = let.let {
            println("let 함수 실행 : $it")
            it.age?.minus(6)
        }
        println(">>> 결과 : $minusSix")

        // 2. 스트림 내 let
        val let2 = mutableListOf(
            LetScope("0001", 1),
            LetScope("0002", 2),
            LetScope("0003", 3))
        let2
            .filter(::isOdd) // 람다 대신 최상위 메서드 레퍼런스
            .map {
                println("age : ${it.age}")
                it.name.toInt() * 3
            }
            .let {
                val test = 1
                println("list + 1 : ${it + test}") // + 연산자의 결과로 read-only collection 이 생성된다.
            }

        // 3. null check
        var nullableLet: LetScope? = null
        nullableLet?.let {
            println("null check")
        }

        // 테스트 중에 발견했음.. 뭔지 더 자세히 알아보자!
        null?.let {
            println("?")
        }
    }
    ```
  
---
## 3. <b>apply</b> <span style="color:gray">*"다음의 지시를 객체에 적용하라(apply the following assignments to the object)."*</spam>
- 객체의 컨텍스트를 참조하는 방식
    - 람자 수신자로써의 컨텍스트를 this 키워드로 참조
    - `apply` 를 사용할 경우 내부 scope 는 this 의 성질을 갖는다.
- 리턴 값
    - 컨텍스트 객체를 리턴한다.
- case
    - 객체 선언
- code
    ```kotlin
    class ApplyScope(val name: String, val age: Int) {
        fun printName() {
            println("Object name : $name")
        }
    }

    fun main() {

        // 1. 람다 수신자
        // 프로퍼티에 바로 접근이 가능하다
        // 스코프 함수 apply 의 타입이 수신 객체 타입이기 때문이다
        val applyScope: ApplyScope = ApplyScope("apply", 1).apply { println("age: $age")}

        // 2. 컨텍스트 객체를 반환하기 때문에 체이닝 방식으로 작성 가능
        // 메서드 참조는 중괄호 없이 사용한다
        applyScope.apply(ApplyScope::printName).apply { println("모든 프로퍼티를 출력했어요!") }

    }
    ```
  
---
## 4. <b>also</b> <span style="color:gray">*"그리고 또한 다음을 수행하라(and also do the following)."*</style>
- 객체의 컨텍스트를 참조하는 방식
    - 컨텍스트 객테를 람자 인자로 가진다.
    - 암시적인 기본 이름인 it 으로 접근이 가능하다.
- 리턴 값
    - 컨텍스트 객체를 리턴한다.
- case
    - 부가적인 실행
- code
    ```kotlin
    data class AlsoScope(val name: String, val age: Int)

    fun main() {

        // 1. 람다 객체를 인자로 받아 it 으로 접근 혹은 다른 이름 지정
        val alsoScope = AlsoScope("also", 55)
            .also { println("AlsoScope 를 생성하였습니다 : $it") }
            .also { also -> println("한번 더 출력 : $also") }
    }
    ```
  
---
## 5. <b>with</b> <span style="color:gray">*"이 객체로, 다음을 수행하라(with this object, do the following.)."*</style>
- 객체의 컨텍스트를 참조하는 방식
    - 람다 수신자로써의 컨텍스트를 this 키워드로 참조
    - `with` 을 사용할 경우 내부 scope 는 this 의 성질을 갖는다.
- 리턴 값
    - 함수 리터럴의 마지막 expression
- 비확장 함수이다.
- case
    - 객체에 대한 그룹 함수 호출
    - 헬퍼 객체의 프로퍼티나 함수를 선언
- code
    ```kotlin
    data class WithScope(val name: String, val age: Int)

    fun main() {

        val with: WithScope = WithScope("with", 25)

        val result = with(with) {
            println("also Scope $name")
            1
        }
        println("${result == 1}")

    }
    ```
  