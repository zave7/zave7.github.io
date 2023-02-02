---
title: Kafka 스트림즈 DSL GlobalKTable KStream Join
categories: Kafka
---

# 스트림즈 DSL - GlobalKtable과 KStream을 join()

order 토픽과 address 토픽은 코파티셔닝되어 있으므로 각각 KTream과 KTable로 선언해서 조인을 할 수 있었다. 

그러나 코파티셔닝 되어있지 않은 토픽을 조인해야할때는 어떻게 해야 할까? 

코파티셔닝되지 않은 데이터를 조인하는 방법은 두 가지가 있다. 

![Untitled](/images/kafka/Untitled%2013.png)

첫 번째는 리파티셔닝을 수행한 이후에 코파티셔닝이 된 상태로 조인 처리를 하는 것이고

두 번째는 KTable로 사용하는 토픽을 GlobalKTable로 선언하여 사용하는 것이다.

- 리파티셔닝은 사용하고 있는 특정 토픽에 있는 파티션을 조인하고자 하는 토픽의 파티션 갯수와 맞춰주는 것이다. 파티션 갯수가 동일한 토픽을 새로 생성해서 사용하는 것이다.
- 데이터가 많지 않다면 글로벌테이블을 사용해서 조인을 수행해서 처리할 수 있다.

- code
    
    ```kotlin
    import java.util.Properties
    import org.apache.kafka.common.serialization.Serdes
    import org.apache.kafka.streams.KafkaStreams
    import org.apache.kafka.streams.StreamsBuilder
    import org.apache.kafka.streams.StreamsConfig
    
    class KStreamJoinGlobalKTable {
        private val APPLICATION_NAME = "global-table-join-application"
        private val BOOTSTRAP_SERVERS = "my-kafka:9092"
        private val ADDRESS_GLOBAL_TABLE = "address_v2"
        private val ORDER_STREAM = "order"
        private val ORDER_JOIN_STREAM = "order_join"
        
        fun streaming() {
            val props = Properties()
            props[StreamsConfig.APPLICATION_ID_CONFIG] = APPLICATION_NAME
            props[StreamsConfig.BOOTSTRAP_SERVERS_CONFIG] = BOOTSTRAP_SERVERS
            props[StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG] = Serdes.String().javaClass
            props[StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG] = Serdes.String().javaClass
    
            val builder = StreamsBuilder()
            val addressGlobalTable = builder.globalTable<String, String>(ADDRESS_GLOBAL_TABLE)
            val orderStream = builder.stream<String, String>(ORDER_STREAM)
    
            orderStream
                .join(
                    addressGlobalTable,
                    { orderKey: String, _: String? -> orderKey },
                    { order: String, address: String -> "$order send to $address" }
                ) 
                .to(ORDER_JOIN_STREAM)
    
            val streams = KafkaStreams(builder.build(), props)
            streams.start()
        }
    }
    
    fun main() {
        KStreamJoinGlobalKTable().streaming()
    }
    ```
    
- shell
    
    ```bash
    # 코파티셔닝 되지 않은 파티션 2개 토픽 생성
    $ bin/kafka-topics.sh --bootstrap-server my-kafka:9092 --partitions 2 --topic address_v2 --create
    
    # address_v2 토픽 메세지 생성
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic address_v2 --property "parse.key=true" --property "key.separator=:"
    > chan:Seoul
    
    # order 토픽 메세지 생성
    $ bin/kafka-console-producer.sh --bootstrap-server my-kafka:9092 --topic order --property "parse.key=true" --property "key.separator=:"
    > chan:Galaxy
    
    # order_join 메세지 컨슘
    bin/kafka-console-consumer.sh --bootstrap-server my-kafka:9092 \
    	--topic order_join \
    	--property print.key=true \
    	--property key.separator=":" \
    	--from-beginning
    
    # join 결과
    chan:Galaxy send to Seoul
    ```