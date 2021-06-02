---
title: kotlin variable
categories: Kotlin
---

# Kotlin Variable
- 코틀린 변수 선언
    - 변수 선언시 키워드 `var` 또는 `val` 를 명시해야한다.
    - `변수명: 타입` 순으로 작성한다.
        ```
        ex) var v1: Int
            val v2: Long
        ```

### 1. var
- var 는 변경 가능한 변수를 선언할 때 사용된다.
    ```kotlin
    fun main() {
        var v: Int = 1
        v = 2 // 변수에 값 재할당 가능
    }
    ```

### 2. val
- val 은 변경 불가능한 변수를 선언할 때 사용된다.
- java 의 final 과 유사하다.
    ```kotlin
    fun main() {
        val v: Int = 1 // 선언과 동시에 값을 할당해줘야 한다.
        v = 3 // 변수에 값 재할당 시 컴파일 에러 발생한다.
    }
    ```

### 3. const val
- const val 키워드는 원시타입(Int, Long 등)과 String 만 넣을 수 있는 완전 상수를 선언하는 것이다.
- Top-Level Constants 혹은 object / companion object 안에만 작성할 수 있다.
    ```kotlin
    const val V: Int = 1 // Top-Level Constants 

    fun main() {
        println(V)
        V = 2 // 컴파일 에러가 발생한다
    }

    object TestSingleton {
        const val V2 = 1
    }

    class Test {
        companion object {
            const val V3 = 1;
        }
    }
    ```

### 4. lateinit var
- lateinit var 는 초기화를 미룬다는 것을 컴파일러에게 알려주는 키워드이다.
- 제약 사항
    - 원시타입은 선언할 수 없다.
    - nullable 타입을 허용하지 않는다.
    - custom property 를 만들 수 없다.
    - 초기화 하지 않고 해당 프로퍼티에 접근 시 `UninitializedPropertyAccessException` 발생
    ```kotlin
    fun main() {
        val lateVal = LateTest()
        lateVal.init(Test(1))
        println(lateVal.test.value)
    }

    data class Test(val value: Int)

    class LateTest {

        lateinit var test : Test // Test? 또는 원시타입 선언 불가

        fun init(test: Test) {
            this.test = test
        }
    }
    ```
- 아래 코드에서는 `Exception in thread "main" kotlin.UninitializedPropertyAccessException: lateinit property test has not been initialized` 이 발생한다.
    ```kotlin
    fun main() {
        val lateVal = LateTest()
        // lateVal.init(Test(1)) 
        println(lateVal.test.value)
    }
    ```
- custom property 선언 불가
    ```kotlin
    class LateTest {

        lateinit var test : Test
        get() { // 컴파일 에러 발생
            test
        }
    }
    ```

### 5. nullable, non-null
- 코틀린은 타입 뒤에 ? 키워드로 Null 허용 여부를 결정한다.