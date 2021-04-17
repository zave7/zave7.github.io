---
title: "JPA fetch size"
categories: Hibernate
---

# JPA fetch size

## # default_batch_fetch_size 옵션
  - 보통 RDB들은 select * from x where in (?) 와 같은 preparedstatement는 미리 문법을 파싱해서 최대한 캐싱을 해둔다.
  - 그런데 데이터가 1개, 2개, 3개, 100개가 있으면 모두 각각 다음 처럼 최대 100개의 preparedstatement 쿼리를 만들어야 한다.
    ```
    select * from x where in (?)
    select * from x where in (?, ?)
    select * from x where in (?, ?, ?)
    select * from x where in (?, ?, ? ...)
    ```
    - 이렇게 되면 DB 입장에서 너무 많은 preparedstatement 쿼리를 캐싱해야 하고, 성능도 떨어지게 된다.
    - 그래서 하이버네이트는 이 문제를 해결하기 위해 내부에서 나름 최적화를 한다.
    ```
    100 = 설정값
    50 = 100/2
    25 = 50/2
    12 = 25/2
    ```
    - 그리고 1~10까지는 자주 사용하니 모두 설정. 이런식으로 잡아둔다.
    
    그러면 기존에 100개의 preparedstatement 모양을
       1~10, 12, 25, 50 ,100 해서 총 14개의 모양으로 최적화를 한다.
       이렇게 해서 100으로 최대값을 설정하고,
       18을 설정하면 12, 6 이렇게 다음과 같이 나누어서 실행된다.

    select * from x where in (?*12)
    select * from x where in (?*6)

    추가로 다음과 같은 속성으로 최적화 전략을 제어할 수 있다.

    spring.jpa.properties.hibernate.batch_fetch_style: legacy //기본
    spring.jpa.properties.hibernate.batch_fetch_style: padded
    spring.jpa.properties.hibernate.batch_fetch_style: dynamic //최적화X

    padded 전략은 링크 참고 : https://docs.jboss.org/hibernate/orm/4.2/manual/en-US/html/ch20.html#performance-fetching-batch
    
### # 참조(출처) 링크 : https://www.inflearn.com/questions/34469
