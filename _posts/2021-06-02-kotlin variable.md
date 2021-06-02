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