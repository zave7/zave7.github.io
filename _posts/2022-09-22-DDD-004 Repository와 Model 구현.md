---
title: DDD 4. Repository와 Model 구현
categories: DDD
---

# ⌜리포지터리와 모델 구현**⌟**

- 같은 라이프 사이클을 갖는 엔티티와 밸류를 묶어 하나의 애그리게이트 엔티티로 매핑한다.
    - 이때, 별도의 밸류 테이블이 있다고 해당 밸류를 엔티티로 인식하기가 쉬운데 밸류는 정말 말 그대로 엔티티에 속한 값일 뿐이고 실제 도메인 모델 엔티티는 루트 엔티티 하나이다.
    - 밸류의 식별자는 DB에서 식별하기 위해 있는 것이지 도메인을 식별하기 위한 식별자는 아니기 때문이다.
- 적용 어노테이션
    - @Entity
        
        주로 루트 엔티티에 지정한다. (밸류를 별도 테이블로 구성했을때 사용하기도 함)
        
    - @Table
        
        테이블 속성 지정 ( 이름 등 )
        
    - @Access
        - JPA는 필드와 프로퍼티의 두 가지 방식으로 매핑을 처리할 수 있다.
        - set 프로퍼티를 구현하지 않기 위해 AccessType 을 Field 로 지정한다.
        - 기본적으로 @Id나 @EmbeddedId 가 위치한 곳에 따라 맞춰서 접근 방식을 선택한다.
        (field 에 선언 시 field 접근, property에 선언 시 property 접근)
    - @Id
        
        Id 에 매핑되는 필드 혹은 프로퍼티에 선언한다.
        
    - @GeneratedValue
        
        Id 생성 전략을 지정한다.
        
    - @Column
        
        DB 컬럼에 대응하는 field 에 선언한다. ( 컬럼 이름, 타입 등 속성 지정 )
        
    - @Enumerated
        
        Enum 타입 필드를 Column 으로 지정할때 사용한다.
        
    - @EmbeddedId
        
        Id를 별도 클래스로 구현했을 때 선언한다. 이 때 IdClass 는 Serializable 를 구현해야 한다.
        
    - @AttributeOverrides
        
        다른 객체를 필드에 선언한 경우 해당 엔티티에서는 다른 컬럼명을 사용하고 싶을 때 선언한다.
        
    - @AttributeOverride
        
        다른 객체를 필드에 선언한 경우 해당 엔티티에서는 다른 컬럼명을 사용하고 싶을 때 선언한다.
        
    - @Embedded
        
        값 타입 필드에 선언한다.
        
    - @Embeddable
        
        값 타입 클래스에 선언한다.
        
    - @Converter
        
        밸류 매핑 클래스에 선언한다. 
        autoApply 속성을 통해 @Convert 어노테이션을 선언하지 않게할 수 도 있다. ( 기본 false )
        
    - @Convert
        
        autoApply 속성이 false 일 때 해당 필드에 선언한다.
        
    - @ElementCollection
        - 필드가 별도의 테이블에 속한 컬렉션임을 선언한다.
        - 부모 Entity Id와 추가 컬럼(basic or embedded 타입)으로 구성된다.
        - 항상 부모와 함께 저장되고 삭제되므로 cascade 옵션은 제공하지 않는다.
        - 기본적으로 식별자 개념이 없으므로 컬렉션 값 변경 시, 전체 삭제 후 새로 추가한다.
    - @CollectionTable
        - @ElementCollection 와 함께 값 타입 컬렉션 필드에 선언한다.
        - 테이블의 이름과 왜래키를 지정한다.
        - 엔티티와 같은 생명주기를 따라간다.
        - 일대다 관계에서 cascade = ALL, orphanRemoval = true 를 설정한 것과 같다.
        - 식별자가 필요하지 않은 정말 단순한 값 타입이라고 판단 될때 사용한다.
        - @Embeddable 이 선언된 클래스 타입의 필드와도 많이 사용된다.
    - @OrderColumn
        
        지정한 컬럼에 리스트의 인덱스 값을 저장한다.
        
    - @JoinColumn
        
        외부키로 사용할 컬럼을 지정한다.
        
    - @SecondaryTable
        
        밸류를 매핑한 테이블을 지정하기 위해 @AttributeOverride, @PrimaryKeyJoinColumn 어노테이션과 함깨 이용한다.
        
    - @PrimaryKeyJoinColumn
        
        밸류 테이블에서 엔티티 테이블로 조인할 때 사용할 컬럼을 지정한다.
        
    - @Inheritance
        
        상속관계 매핑을 위해 선언한다. 여러 전략이 존재한다.
        
    - @DiscriminatorColumn
        
        부모 클래스에 선언한다. 하위 클래스를 구분하는 용도의 컬럼이다. (관례 default = DTYPE)
        
    - @DiscriminatorValue
        - 하위 클래스에 선언한다. 엔티티를 저장할 때 슈퍼타입의 구분 컬럼에 저장할 값을 지정한다.
        - 선언하지 않을 경우 기본값으로 클래스 이름이 들어간다.
    - @Temporal
        - DB 날짜 컬럼 타입 유형에 맞도록 지정한다. 기본값은 TIMESTAMP 이다.
        - TemporalType.DATE : 년-월-일 의 date 타입
        - TemporalType.TIME : 시-분-초 의 time 타입
        - TemporalType.TIMESTAMP : date + time timestamp(datetime) 타입
    - @OneToMany
        
        1 : N 관계 매핑 전략
        
    - @ManyToOne
        
        N : 1 관계 매핑 전략
        
    
- 값 타입이 아닌 애그리거트의 루트 엔티티의 ID는 모두 EmbeddedId 로 가져가는게 좋아보인다.
추후 하위 도메인이 별도의 시스템으로 분리될 때 ID 참조 방식으로 서로 다른 애그리거트를 조회하게 될 텐데 
이때 ID 가 타입으로 되어있는 것이 가독성과 안전성에 있어서 큰 효과를 주는것 같다.

## 애그리거트 로딩 전략

- JPA 매핑을 설정할 때 항상 기억해야할 것은 애그리거트에 속한 객체가 모두 모여야 완전한 하나가 된다는 것이다.
- 하지만 조회와 상태 변경 기능, 이 두 가지 경우를 분리해서 생각해야한다.

## 애그리거트의 영속성 전파

- @Embeddable 타입일 경우 값 타입이기 때문에 자동 cascade 이다.
- 반면 @Entity 타입일 경우 persist, remove 영속성 설정이 필요하다.

## 식별자 생성 기능

- 사용자가 직접 생성
- 도메인 로직으로 생성
- DB를 이용한 일련번호 사용

## 도메인 구현과 DIP

- DIP에 따르면 도메인 모델은 구현 기술에 의존하지 말아야 한다.
즉, 도메인이 인프라에 의존하면 안된다.