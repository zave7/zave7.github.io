---
title: MariaDB 테이블 파티셔닝
categories: DB
---

# 파티셔닝에서 사용할 수 있는 함수
  - 공식문서주소 : https://dev.mysql.com/doc/refman/8.0/en/partitioning-limitations-functions.html
  
## 주요 용어
  1. 파티션 프루닝 : 접근이 불필요한 파티션은 전혀 접근하지 않는것, 실행계획은 EXPLAIN PARTITIONS 를 사용
    - 정상적인 프루닝을 지원하는 함수는 YEAR(), TO_DAYS(), TO_SECOND() (5.5이상) 단 3개 뿐이다.

### List 파티셔닝
  1. List 파티셔닝에서는 파티션 생성 시 'VALUES IN' 을 사용하면 된다.
  ```
  PARTITION BY LIST COLUMNS(YEAR(day_of_date)) (
  PARTITION p2021 VALUES IN (2021)
  );
  ```
### Range 파티셔닝
  1. Range 파티셔닝에서는 파티션 생성 시 'VALUES LESS THAN' 을 사용하면 된다.
  2. 'VALUES THAN MAXVALUE' 를 사용하여 나머지 값을 파티셔닝 할 수 있다.
  
### Hash 파티셔닝
  
### 서브 파티셔닝

### 기존 테이블에 파티션 생성
  ```
  ALTER TABLE table_name PARTITION BY RANGE COLUMNS(day_of_date) (
	PARTITION p2021 VALUES LESS THAN ('20211231'),
	PARTITION p2022 VALUES LESS THAN ('20221231'),
	PARTITION p2023 VALUES LESS THAN ('20231231')
  );
  ```
  
### 기존 파티션에 추가
  ```
  ALTER TABLE table_name ADD PARTITION (
  PARTITION p2017 VALUES LESS THAN ('20171231')
  );
  ```
### 테이블 파티셔닝 조회
  ```
  SELECT *
  FROM information_schema.partitions
  WHERE TABLE_NAME = 'table_name';
  ```

### 특정 파티션 조회
  ```
  SELECT * FROM table_name PARTITION (p2021);
  ```
### 파티션 제거
  1. 파티션 별 제거
      ```
      ALTER TABLE table_name DROP PARTITION p2021
      ```
  2. 모든 파티션 제거
    - 파티션이 하나 남았을때는 무조건 REMOVE 로 파티션 자체를 지워야 한다.
	    ```
	    ALTER TABLE table_name REMOVE PARTITIONING;
	    ```
### 특정 파티션의 데이터를 truncate 하는 방법
  ```
  ALTER TABLE table_name TRUNCATE PARTITION (p2020);
  ```
