---
title: kotlin kapt 문제
categories: Kotlin
---

# kapt란
- `kapt (annotation processing for kotlin)` 는 코틀린이 자바의 어노테이션을 처리할 때 kotlin 파일의 어노테이션 처리를 포함합니다. JVM을 기동시킬 때 Kotlin의 어노테이션을 포함시키이 위해 사용되는 플러그인입니다.
- 기존 `annotationProcessor` 대신 사용하면된다.

### 호환 문제 (jdk16)
- 현재 kapt 는 jdk16+ 와 호환되지 않고 있다.
- kapt 를 사용하는 querydsl 같은 디펜던시를 사용하지 못한다.
- 관련 링크 : https://youtrack.jetbrains.com/issue/KT-45545

### KSP 
- `kapt` 를 대신하는 `KSP` API
    - 코틀린 1.4.30 버전 이상부터 호환되며 `kapt` 에 비해 최대 2배 이상 빠르다고 한다.
- KSP Github link : https://github.com/google/ksp
- 참조 링크 : https://www.charlezz.com/?p=45255