---
title: Kafka shell script (1)
categories: Kafka
---

# 카프카 shell script (CLI) (1)

### **kafka-topics.sh**

클러스터 정보와 토픽 이름은 토픽을 만들기 위한 필수 값이다.
이렇게 만들어진 토픽은 파티션 갯수, 복제 갯수 등과 같이 다양한 옵션이 포함되어 있지만 모두 브로커에 설정된 기본 값으로 생성된다.

- 토픽 생성
    
    ```bash
    $ bin/kafka-topics.sh --create \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka
    ```
    
- 토픽 정보 조회
    
    ```bash
    $ bin/kafka-topics.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--describe
    ```
    
- 추가적인 옵션 생성
    
    ```bash
    $ bin/kafka-topics.sh --create \
    	--bootstrap-server my-kafka:9092 \
    	--partitions 10 \
    	--replication-factor 1 \
    	--topic hello.kafka2 \
    	--config retention.ms=172800000
    ```
    
- 토픽 리스트 조회
    
    ```bash
    $ bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
    ```
    
- 파티션 갯수 늘리기 (--alter)
    
    ```bash
    $ bin/kafka-topics.sh --create --bootstrap-server localhost:9092 \
    	--topic test # 토픽 생성
    $ bin/kafka-topics.sh --bootstrap-server localhost:9092 \
    	--topic test --describe # 토픽 정보 조회
    $ bin/kafka-topics.sh --bootstrap-server localhost:9092 --topic test \
    	--alter --partitions 4 # 토픽 구성 수정
    $ bin/kafka-topics.sh --bootstrap-server localhost:9092 \
    	--topic test --describe # 토픽 정보 조회
    ```
    
    - 파티션 갯수를 늘릴 수 있지만 줄일 수는 없다. 다시 줄이는 명령을 내리면 InvalidPartitionsException 익셉션이 발생한다. 만약 피치 못할 사정으로 파티션 갯수를 줄여야 할 때는 토픽을 새로 만드는 편이 좋다.
        
        ```bash
        $ bin/kafka-topics.sh --bootstrap-server localhost:9092 --topic test \
        	--alter --partitions 2 # 파티션 숫자 줄이기
        
        # 에러 발생
        ERROR java.util.concurrent.ExecutionException: 
        	org.apache.kafka.common.errors.InvalidPartitionsException: 
        	Topic currently has 4 partitions, which is higher than the requested 2.
        ```
        

### **kafka-configs.sh**

토픽의 일부 옵션을 설정하기 위해서는 kafka-configs.sh 명령어를 사용해야한다.
--alter 와 --add-config 옵션을 사용하여 min.insync.replicas 옵션을 토픽별로 설정할 수 있다.
또한 브로커에 설정된 각종 기본값은 --broker, --all, --describe 옵션을 사용하여 조회할 수 있다.

- min.insync.replicas 설정
    
    ```bash
    $ bin/kafka-configs.sh --bootstrap-server my-kafka:9092 \
    	--alter \
    	--add-config min.insync.replicas=2 \
    	--topic test
    ```
    
- 브로커 설정 값 조회
    
    ```bash
    $ bin/kafka-configs.sh --bootstrap-server my-kafka:9092 \
    	--broker 0 \
    	--all \
    	--describe
    ```
    

### **kafka-console-producer.sh**

개발하면서 많이 사용된다. 카프카 토픽의 테스트 용도로 많이 사용된다.
키보드로 문자를 작성하고 엔터 키를 누르면 별다른 응답 없이 메세지 값이 전송된다.

- 메세지 전송
    
    ```bash
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    >hello
    >kafka
    >0
    >1
    >2
    >3
    >4
    >5
    >6
    # 입력값은 메세지 값으로 전송된다. key에 대한 설정이 없으므로 key는 null로 전송된다.
    ```
    
- 키와 함께 메세지 전송
    - --property 옵션의 `parse.key=true` , `key.separator=:` 를 설정하면 된다.
    - `key.separator=:` 의 기본 값은 Tab delimiter(￦t) 이므로 별도 선언 없이 보내려면 키를 작성하고 탭키를 누를 뒤 메세지 값을 작성하고 엔터를 누른다.
    
    ```bash
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--property "parse.key=true" \
    	--property "key.separator=:"
    >key1:no1
    >key2:no2
    >key3:no3
    ```
    
    - 같은 메세지 키로 보내진 레코드는 파티셔너에 의해 동일한 파티션에 전송된다. 그러므로 동일한 메세지 키에 대한 레코드는 순서를 지킬 수 있게 된다.
    - 메세지 키가 null 인 경우에는 레코드 배치 단위(레코드 전송 묶음)로 라운드 로빈으로 전송한다.

### **kafka-console-consumer.sh**

테스트 및 개발에서 많이 사용되는 컨슈머 역할 커맨드이다. 특정 토픽의 데이터를 컨슘해서 임시적으로 조회하기 위한 용도이다.

필수 옵션은 카프카 클러스터 정보(--bootstrap-server), 토픽 이름(--topic)이다.
추가로 `--from-beginning` 옵션을 주면 토픽에 저장된 가장 처음 데이터부터 출력한다.

- 토픽으로 전송한 데이터 조회 (메세지 값만 조회)
    
    ```bash
    $ bin/kafka-console-consumer.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--from-beginning
    
    2
    3
    4
    no1
    no2
    ```
    
- 토픽으로 전송한 데이터 조회 (메세지 키와 함께 조회)
- `property` 옵션 지정
    
    ```bash
    $ bin/kafka-console-consumer.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--from-beginning \
    	--property print.key=true \
    	--property key.separator="-"
    
    null-2
    null-3
    null-4
    key1-no1
    key2-no2
    ```
    
- 최대 컨슘 메세지 갯수 지정
- `--max-messages {갯수}` 옵션 지정
    
    ```bash
    $ bin/kafka-console-consumer.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--from-beginning \
    	--max-messages 1
    
    2
    ```
    
- 특정 파티션만 컨슘
- `--partition {번호}` 옵션 지정
    
    ```bash
    $ bin/kafka-console-consumer.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--from-beginning \
    	--partition 2
    
    2
    3
    4
    no1
    no2
    ```
    
- 컨슈머 그룹 기반 컨슘
- 어떤 특정 오프셋 까지 데이터를 읽었다는 것을 커밋시키기 위한 그룹 지정 (그룹별 커밋)
- 컨슈머 그룹으로 토픽의 레코드를 가져갈 경우 어느 레코드 까지 읽었는지에 대한 데이터가 카프카 브로커에 저장된다.
- `--group {그룹명}`  옵션 지정
    
    ```bash
    $ bin/kafka-console-consumer.sh \
    	--bootstrap-server my-kafka:9092 \
    	--topic hello.kafka \
    	--group hello-group \
    	--from-beginning
    
    # 첫번째 컨슘 시에 __consumer_offsets 토픽 에 데이터가 커밋된다.
    $ bin/kafka-topics.sh --bootstrap-server my-kafka:9092 --list
    __consumer_offsets
    hello.kafka
    hello.kafka2
    test
    
    # 두번 이상 실행할 경우 데이터가 컨슘되지 않는다.
    ```
    

### **kafka-consumer-groups.sh**

컨슈머 그룹은 따로 생성하는 명령을 날리지 않고 컨슈머를 동작할 때 컨슈머 그룹 이름을 지정하면 새로 생성된다.
생성된 컨슈머 그룹의 리스트는 kafka-consumer-group.sh 명령어로 확인할 수 있다.

--describe 옵션을 사용하면 해당 컨슈머 그룹이 어떤 토픽을 대상으로 레코드를 가져갔는지 상태를 확인 할  수 있다. 파티션 번호, 현재까지 가져간 레코드의 오프셋, 파티션 마지막 레코드의 오프셋, 컨슈머 랙, 컨슈머 ID, 호스트를 알 수 있기 때문에 컨슈머의 상태를 조회할 때 유용하다.

컨슈머 랙 = 현재까지 가져간 레코드의 오프셋 - 파티션 마지막 레코드의 오프셋
컨슈머 랙의 모니터링이 중요하다.

- 컨슈머 그룹 상태 조회
    
    ```bash
    $ bin/kafka-consumer-groups.sh \
    	--bootstrap-server my-kafka:9092 \
    	--group hello-group \
    	--describe
    
    GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
    hello-group     hello.kafka     2          5               5               0               -               -               -
    hello-group     hello.kafka     1          4               4               0               -               -               -
    hello-group     hello.kafka     0          2               2               0               -               -               -
    ```
    
- 오프셋 리셋
    
    --to-earliest : 가장 처음 오프셋(작은 번호)으로 리셋
    --to-lastest : 가장 마지막 오프셋(큰 번호)으로 리셋
    --to-current : 현 지섬 기준 오프셋으로 리셋
    --to-datetime {YYYY-MM-DDTHH:mm:SS.sss} : 특정 일시로 오프셋 리셋(레코드 타임스탬프 기준)
    --to-offset {long} : 특정 오프셋으로 리셋
    --shift-by {+/- long} : 현재 컨슈머 오프셋에서 앞뒤로 옮겨서 리셋
    
    ```bash
    # 컨슈머 그룹 조회
    $ bin/kafka-consumer-groups.sh \
    	--bootstrap-server my-kafka:9092 \
    	--group hello-group \
    	--describe
    
    GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
    hello-group     hello.kafka     2          5               5               0               -               -               -
    hello-group     hello.kafka     1          4               4               0               -               -               -
    hello-group     hello.kafka     0          2               2               0               -               -               -
    
    # 제일 작은 오프셋으로 리셋
    $ bin/kafka-consumer-groups.sh \
    	--bootstrap-server my-kafka:9092 \
    	--group hello-group \
    	--topic hello.kafka \
    	--reset-offsets --to-earliest --execute
    
    GROUP                          TOPIC                          PARTITION  NEW-OFFSET
    hello-group                    hello.kafka                    0          0
    hello-group                    hello.kafka                    1          0
    hello-group                    hello.kafka                    2          0
    
    # 컨슈머 그룹 다시 조회
    GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
    hello-group     hello.kafka     2          0               5               5               -               -               -
    hello-group     hello.kafka     1          0               4               4               -               -               -
    hello-group     hello.kafka     0          0               2               2               -               -               -
    ```
    
    - 운영 환경에 따라 필요한 오프셋 작업에 사용할 수 있다. (데이터 재처리)