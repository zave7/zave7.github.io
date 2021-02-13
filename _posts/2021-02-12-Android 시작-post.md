---
title: "Android 시작"
categories: Android
---

# Android

## 레이아웃

### Fragment
  - 액티비티 대신 프래그먼트를 만든다
  - 안드로이드 젯팩에서 제공하는 네비게이션이라는 컴포넌트를 이용해서 만든다.
  - 화면간 이동, 트랙잭션 같은것들을 네비게이션이 다 처리를 해준다.

### Constraint Layout
  - 기본적으로 constraint layout을 사용한다.
  - 부득이한 경우가 아니면 리니어 레이아웃과 relative 레이아웃을 사용하지 않는다.
  
### 이미지 경로
  - app\src\main\res\drawable

### 코틀린 사용시 유용한 라이브러리
  - anko : https://github.com/Kotlin/anko
  
### nav_graph
  - fragment 사이의 관계를 정의
  - fragment 의 tools:context 를 제대로 설정해줘야한다.
  
### 코틀린 익스텐션 플러그인
  - 자바에서 사용했었던 findViewById() 대신에 kotlin-android-extensions 플러그인을 사용하여 편리하게 사용할 수 있다.
  - 하지만 2021년에 코틀린 안드로이드 익스텐션은 폐기될 예정이다. 그 이유는 팀은 새롭게 권장되는 구현인 뷰 바인딩 사용을 장려하기 위함이다.
  - Parcelize 기능의 API 및 어노테이션은 유지되므로 계속해서 사용할 수 있다. 단, 어노테이션 패키지 이름이 kotlinx.parcelize로 변경되며 android-kotlin-extension 대신 kotlin-parcelize 플러그인을 대신 사용해야 한다. Parcelize에 대한 추가 내용은 안드로이드 개발자 문서에서 확인할 수 있다. https://developer.android.com/kotlin/parcelize
  
