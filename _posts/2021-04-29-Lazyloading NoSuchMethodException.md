---
title: JPA Lazyloading 시 NoSuchMethodException 발생
categories: Hibernate
---

# 1. 문제
1. 신규 Entity 추가
2. 다른 엔티티에서 해당 엔티티를 `@JoinColum` 으로 매핑 후 Lazyloading 시에 초기화가 되지 않는다는 NoSuchMethodException 발생
    - `Caused by: java.lang.NoSuchMethodException: com.test.spring.user.repository.domain.TestUser$HibernateProxy$3trHAgrm.<init>()`

# 2. 원인
1. Hibernate는 fetch type 이 Lazy 인 프로퍼티에 프록시 객체를 임의로 생성하여 주입해 두고 사용하려고 호출이 될때 실제 Entity 를 생성하여 준다.
2. 기본생성자로 생성하려고하는데 없어서 발생하는 익셉션이었다.

# 3. 해결
- 추가한 Entity 클래스에 기본생성자 작성해서 해결!