---
title: 기존 Java Springboot 프로젝트에 Kotlin 도입
categories: Springboot
---
# Java 프로젝트에 Kotlin 을 추가하게 된 계기
- 기존 프로젝트는 스프링부트 + JPA 로 구성되어있어 생산성이 비교적 좋아졌다.
- 그렇지만 현재 다른 언어들과 같이 모던하지 못한 문법 때문에 불편함을 느꼈고 특히 자바 8에서 Optional 나왔음에도  완전히 Null-Safe 하지는 못하기 때문에 코틀린을 적용하고자 했다.

### 1. Kotlin과 Java 컴파일 시점
- Java 코드와 Kotlin 코드의 빌드 과정은 다음과 같은 순서로 이루어진다.
    1. Kotlin 컴파일러가 Kotlin 코드를 컴파일해 .class 파일을 생성한다. 이 과정에서 Kotlin 코드가 참조하는 Java 코드가 함께 로딩되어 사용된다.
    2. Java 컴파일러가 Java코드를 컴파일 해 .class 파일을 생성한다. 이때 이미 Kotlin이 컴파일한 .class 파일의 경로를 클래스 패스에 추가해 컴파일한다.
- [Naver D2 Kotlin 도입 과정에서 만난 문제와 해결 방법](https://d2.naver.com/helloworld/6685007)

- 이 같은 이유로 컴파일 시점의 차이 때문에 기타 플러그인이나 라이브러리가 중간에 있을 경우 컴파일 단계에서 오류가 발생할 수 있다.

### 2. Lombok 제거
1. Lombok 라이브러리는 자바 컴파일 과정에서 Annotaion Processing 단계에서 적용된다. 그렇기 때문에 Kotlin 코드가 컴파일 된 이후에 적용되기 때문에 Kotlin 코드는 Lombok이 생성한 코드를 사용할 수 없게 되어버린다.
3. Java 와 Kotlin 을 별도 모듈로 분리하면 Lombok 문제는 해결되지만 Java 코드에서 Kotlin 코드를 호출하거나 Kotlin 코드에서 Java 코드를 호출하는 것이 불가능해진다.
4. Delombok 이라는 Lombok이 제공하는 기능을 활용해 프로젝트 빌드 전에 코드를 미리 생성하게 할 수 있지만 빌드 구성이 복잡해진다고 한다.
- 따라서 Lombok 코드를 일괄 제거 하기로 했다.

### 3. Querydsl (build.gradle)
1. 기존 자바만 사용하여 Querydsl을 사용하는 빌드 구성으르 그대로 가져가면 JPA 엔티티 클래스의 쿼리타입이 생성되지 않는다. 그 이유는 Java 컴파일러가 Annotation Processing을 실행하는 과정에서 Kotlin 코드를 인지 할 수없기 때문이다.
2. 따라서 다음과 같이 Kotlin의 Annotation Processing을 지원하도록 다음과 같이 kapt 플러그인을 적용해야한다.
    ```groovy
    plugins {
        id 'org.jetbrains.kotlin.kapt' version '버전'
    }

    dependencies {
        kapt "com.querydsl:querydsl-apt:[querydslversion]:jpa" // 대괄호 부분에 해당하는 querydsl 버전을 기입
    }
    ```
3. 그리고 이전에 플러그인 방식으로 적용 했었던 querydsl 설정은 제거한다.
    ```groovy
    plugins {

        // 제거
        // id "com.ewerk.gradle.plugins.querydsl" version "버전"
    }

    ```
4. 나머지 querydsl 관련 gradle 설정을 제거한다.
    ```groovy
    dependencies {
        implementation 'com.querydsl:querydsl-jpa' // 이 의존성만 남겨놓고 나머지 모두 제거
    }
    ```

5. 최종 build.gradle
    ```groovy
    plugins {
        id 'org.springframework.boot' version '2.3.4.RELEASE'
        id 'io.spring.dependency-management' version '1.0.10.RELEASE'
        id 'java'
        // kotlin 플러그인
        id 'org.jetbrains.kotlin.jvm' version '1.5.0-RC'
        id 'org.jetbrains.kotlin.kapt' version '1.5.0-RC'
        // 스프링 연동시 코틀린을 위한 플러그인 추가 (open, 기본생성자)
        id "org.jetbrains.kotlin.plugin.allopen" version "1.5.0"
        id "org.jetbrains.kotlin.plugin.noarg" version "1.5.0"
    }

    sourceCompatibility = '11'
    targetCompatibility = '11'

    compileKotlin {
        kotlinOptions {
            jvmTarget = "11"
        }
    }

    compileTestKotlin {
        kotlinOptions {
            jvmTarget = "11"
        }
    }

    repositories {
        mavenCentral()
    }

    ext {
        kotlinVersion = '1.5.0-RC'
        queryDslVersion = '4.3.1'
    }

    dependencies {

        // 스프링부트 의존성 생략..

        // kapt 버전과 jpa 까지 꼭 적어줘야 한다!!
        kapt "com.querydsl:querydsl-apt:${queryDslVersion}:jpa" 

        implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk8:${kotlinVersion}"

        // querydsl 의존성 추가
        implementation 'com.querydsl:querydsl-jpa'
    }

    // AllOpen 을 위한 어노테이션 지정
    allOpen {
        annotation("com.test.project.common.plugin.KotlinAllOpen")
    }

    // 기본 생성자 생성을 위한 어노테이션 지정
    noArg {
        annotation("com.test.project.common.plugin.KotlinNoArgsConstructor")
    }

    test {
        useJUnitPlatform()
    }
    ```

### 3-1. kotlin class 'cannot find symbol' 문제
- 진짜 문제는 여기서 부터 시작이었다.
1. gradle 빌드 시에 compileQuerydsl task 를 수행하는 시점에 Java 코드에서 Kotlin 클래스 파일을 참조하는 부분에서 계속 `cannot find symbol` 오류가 발생했다. 구글링을 많이 시도해봤지만 대부분이 위와 관련된 설정에 대한 가이드였고 비슷한 케이스 조차 발견하지 못했다.
    - 아래와 비슷한 에러가 출력된다.
        ```
        Incremental annotation processing requested, but support is disabled because the following processors are not incremental: com.querydsl.apt.jpa.JPAAnnotationProcessor (NON_INCREMENTAL)
        ```
    - 그리고 JDK 컴파일러로 재컴파일 한다는 문구도 출력된다. 바로 이 부분에서 kotlin 클래스 파일을 인식하지 못하는것이다.
    - JPAAnnotationProcessor 가 증분 주석처리를 하지 못했고 그래서 전체 JDK Java 컴파일러가 전체 재컴파일을 시도한다.
    - 컴파일을 할때 컴파일된 코틀린 class 파일이 클래스 패스에 존재하지 않으니 코틀린 파일을 인식하지 못하여 `cannot find symbol` 에러를 출력하는것 같다.

2. Gradle 버전 업그레이드로 해결
    - gradle 5.6.4 버전의 증분 주석처리 지원이 되지 않는 문제인것 같다.
    - 프로젝트 내부에서 아래 커맨드를 실행하여 6.7.1 버전으로 올렸다.
        ```
        gradlew wrapper --gradle-version 6.7.1
        ```
