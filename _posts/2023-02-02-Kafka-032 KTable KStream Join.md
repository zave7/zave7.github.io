---
title: Kafka 스트림즈 DSL KTable KStream Join
categories: Kafka
---

# 스트림즈 DSL - Ktable과 KStream을 join()

KTable과 KStream은 메세지 키를 기준으로 조인할 수 있다. 

대부분의 데이터베이스는 정적으로저장된 데이터를 조인하여 사용했지만 카프카에서는 실시간으로 들어오는 데이터들을 조인할 수 있다. 

사용자의 이벤트 데이터를 데이터베이스에 저장하지 않고도 조인하여 스트리밍 처리할 수 있다는 장점이 있다. 이를 통해 이벤트 기반 스트리밍 데이터 파이프라인을 구성할 수 있는 것이다.

![Untitled](/images/kafka/Untitled%2010.png)

이름을 메세지 키, 주소를 메세지 값으로 가지고 있는 KTable이 있고 이름을 메세지 키, 주문할 물품을 메세지 값으로 가지고 있는 KStream이 존재한다고 가정하자. 

사용자가 물품을 주문하면 이미 토픽에 저장된 `이름:주소` 로 구성된 KTable과 조인하여 물품과 주소가 조합된 데이터를 새로 생성할 수 있다.

![Untitled](/images/kafka/Untitled%2011.png)

만약 사용자의 주소가 변경되는 경우엔 어떻게 될까?

KTable은 동일한 메세지 키가 들어올 경우 가장 마지막의 레코드를 유효한 데이터로 보기 때문에 가장 최근에 바뀐 주소로 조인을 수행할 것이다.

![Untitled](/images/kafka/Untitled%2012.png)

- code
    
    ```kotlin
    import java.util.Properties
    import org.apache.kafka.common.serialization.Serdes
    import org.apache.kafka.streams.KafkaStreams
    import org.apache.kafka.streams.StreamsBuilder
    import org.apache.kafka.streams.StreamsConfig
    
    class KStreamJoinKTable {
        private val APPLICATION_NAME = "order-join-application"
        private val BOOTSTRAP_SERVERS = "my-kafka:9092"
        private val ADDRESS_TABLE = "address"
        private val ORDER_STREAM = "order"
        private val ORDER_JOIN_STREAM = "order_join"
    
        fun streaming() {
            val props = Properties()
            props[StreamsConfig.APPLICATION_ID_CONFIG] = APPLICATION_NAME
            props[StreamsConfig.BOOTSTRAP_SERVERS_CONFIG] = BOOTSTRAP_SERVERS
            props[StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG] = Serdes.String().javaClass
            props[StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG] = Serdes.String().javaClass
    
            val builder = StreamsBuilder()
            val addressTable = builder.table<String, String>(ADDRESS_TABLE)
            val orderStream = builder.stream<String, String>(ORDER_STREAM)
            orderStream
                .join(addressTable) {
                    order, address -> "$order send to $address"
                }
                .to(ORDER_JOIN_STREAM)
    
            val kafkaStreams = KafkaStreams(builder.build(), props)
            kafkaStreams.start()
        }
    }
    
    fun main() {
        KStreamJoinKTable().streaming()
    }
    ```
    
- shell
    
    ```bash
    # 토픽 생성
    $ bin/kafka-topics.sh --bootstrap-server my-kafka:9092 --partitions 3 --topic address --create
    $ bin/kafka-topics.sh --bootstrap-server my-kafka:9092 --partitions 3 --topic order --create
    $ bin/kafka-topics.sh --bootstrap-server my-kafka:9092 --partitions 3 --topic order_join --create
    
    # address, order 토픽 데이터 추가
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic address --property "parse.key=true" --property "key.separator=:"
    >chan:Seoul
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic order --property "parse.key=true" --property "key.separator=:"
    >chan:iPhone
    
    # order_join 토픽 컨슘
    $ bin/kafka-console-consumer.sh --bootstrap-server my-kafka:9092 \
    	--topic order_join \
    	--property print.key=true \
    	--property key.separator=":" \
    	--from-beginning
    
    # join 된 결과
    chan:iPhone send to Seoul
    
    # 같은 메세지 키의 address 토픽 메세지 생성
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic address --property "parse.key=true" --property "key.separator=:"
    >chan:Busan
    # order stream 토픽 메세지 생성
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic order --property "parse.key=true" --property "key.separator=:"
    >chan:iPhone
    
    # join 된 결과
    chan:iPhone send to Busan
    ```