---
title: Kotlin Function
categories: Kotlin
---

# Kotlin Function

### 1. Entry Point
- 코틀린 애플리케이션의 엔트리 포인트는 `main function` 이다.
    ```kotlin
    fun main() {
        println("Hello world!")
    }
    ```

### 2. Function 작성
- 설명
    ```kotlin
    fun 함수이름(매개변수...) : 리턴타입 {
        // Statement
    }
    ```
- 작성 예시
    ```kotlin
    fun sum(a: Int, b: Int): Int {
        return a + b
    }
    ```
    