---
title: Kafka shell script (2)
categories: Kafka
---

### **kafka-producer-perf-test.sh**

카프카 프로듀서로 퍼포먼스를 측정할 때 사용된다.

```bash
$ bin/kafka-producer-perf-test.sh \
    --producer-props bootstrap.servers=my-kafka:9092 \
    --topic hello.kafka \
    --num-records 10 \
    --throughput 1 \
    --record-size 100 \
    --print-metric

7 records sent, 1.3 records/sec (0.00 MB/sec), 59.7 ms avg latency, 300.0 ms max latency.
10 records sent, 1.071811 records/sec (0.00 MB/sec), 46.10 ms avg latency, 300.00 ms max latency, 17 ms 50th, 300 ms 95th, 300 ms 99th, 300 ms 99.9th.
```

- 상세 로그
    
    ```bash
    Metric Name                                                                           Value
    app-info:commit-id:{client-id=producer-1}                                           : 66563e712b0b9f84
    app-info:start-time-ms:{client-id=producer-1}                                       : 1672481164447
    app-info:version:{client-id=producer-1}                                             : 2.5.0
    kafka-metrics-count:count:{client-id=producer-1}                                    : 102.000
    producer-metrics:batch-size-avg:{client-id=producer-1}                              : 182.111
    producer-metrics:batch-size-max:{client-id=producer-1}                              : 279.000
    producer-metrics:batch-split-rate:{client-id=producer-1}                            : 0.000
    producer-metrics:batch-split-total:{client-id=producer-1}                           : 0.000
    producer-metrics:buffer-available-bytes:{client-id=producer-1}                      : 33554432.000
    producer-metrics:buffer-exhausted-rate:{client-id=producer-1}                       : 0.000
    producer-metrics:buffer-exhausted-total:{client-id=producer-1}                      : 0.000
    producer-metrics:buffer-total-bytes:{client-id=producer-1}                          : 33554432.000
    producer-metrics:bufferpool-wait-ratio:{client-id=producer-1}                       : 0.000
    producer-metrics:bufferpool-wait-time-total:{client-id=producer-1}                  : 0.000
    producer-metrics:compression-rate-avg:{client-id=producer-1}                        : 1.000
    producer-metrics:connection-close-rate:{client-id=producer-1}                       : 0.000
    producer-metrics:connection-close-total:{client-id=producer-1}                      : 0.000
    producer-metrics:connection-count:{client-id=producer-1}                            : 2.000
    producer-metrics:connection-creation-rate:{client-id=producer-1}                    : 0.051
    producer-metrics:connection-creation-total:{client-id=producer-1}                   : 2.000
    producer-metrics:failed-authentication-rate:{client-id=producer-1}                  : 0.000
    producer-metrics:failed-authentication-total:{client-id=producer-1}                 : 0.000
    producer-metrics:failed-reauthentication-rate:{client-id=producer-1}                : 0.000
    producer-metrics:failed-reauthentication-total:{client-id=producer-1}               : 0.000
    producer-metrics:incoming-byte-rate:{client-id=producer-1}                          : 38.085
    producer-metrics:incoming-byte-total:{client-id=producer-1}                         : 1491.000
    producer-metrics:io-ratio:{client-id=producer-1}                                    : 0.001
    producer-metrics:io-time-ns-avg:{client-id=producer-1}                              : 1555532.528
    producer-metrics:io-wait-ratio:{client-id=producer-1}                               : 0.229
    producer-metrics:io-wait-time-ns-avg:{client-id=producer-1}                         : 250237896.889
    producer-metrics:io-waittime-total:{client-id=producer-1}                           : 9008564288.000
    producer-metrics:iotime-total:{client-id=producer-1}                                : 55999171.000
    producer-metrics:metadata-age:{client-id=producer-1}                                : 9.107
    producer-metrics:network-io-rate:{client-id=producer-1}                             : 0.613
    producer-metrics:network-io-total:{client-id=producer-1}                            : 24.000
    producer-metrics:outgoing-byte-rate:{client-id=producer-1}                          : 59.545
    producer-metrics:outgoing-byte-total:{client-id=producer-1}                         : 2331.000
    producer-metrics:produce-throttle-time-avg:{client-id=producer-1}                   : 0.000
    producer-metrics:produce-throttle-time-max:{client-id=producer-1}                   : 0.000
    producer-metrics:reauthentication-latency-avg:{client-id=producer-1}                : NaN
    producer-metrics:reauthentication-latency-max:{client-id=producer-1}                : NaN
    producer-metrics:record-error-rate:{client-id=producer-1}                           : 0.000
    producer-metrics:record-error-total:{client-id=producer-1}                          : 0.000
    producer-metrics:record-queue-time-avg:{client-id=producer-1}                       : 2.556
    producer-metrics:record-queue-time-max:{client-id=producer-1}                       : 15.000
    producer-metrics:record-retry-rate:{client-id=producer-1}                           : 0.000
    producer-metrics:record-retry-total:{client-id=producer-1}                          : 0.000
    producer-metrics:record-send-rate:{client-id=producer-1}                            : 0.256
    producer-metrics:record-send-total:{client-id=producer-1}                           : 10.000
    producer-metrics:record-size-avg:{client-id=producer-1}                             : 186.000
    producer-metrics:record-size-max:{client-id=producer-1}                             : 186.000
    producer-metrics:records-per-request-avg:{client-id=producer-1}                     : 1.111
    producer-metrics:request-latency-avg:{client-id=producer-1}                         : 14.444
    producer-metrics:request-latency-max:{client-id=producer-1}                         : 26.000
    producer-metrics:request-rate:{client-id=producer-1}                                : 0.306
    producer-metrics:request-size-avg:{client-id=producer-1}                            : 194.250
    producer-metrics:request-size-max:{client-id=producer-1}                            : 340.000
    producer-metrics:request-total:{client-id=producer-1}                               : 12.000
    producer-metrics:requests-in-flight:{client-id=producer-1}                          : 0.000
    producer-metrics:response-rate:{client-id=producer-1}                               : 0.307
    producer-metrics:response-total:{client-id=producer-1}                              : 12.000
    producer-metrics:select-rate:{client-id=producer-1}                                 : 0.916
    producer-metrics:select-total:{client-id=producer-1}                                : 36.000
    producer-metrics:successful-authentication-no-reauth-total:{client-id=producer-1}   : 0.000
    producer-metrics:successful-authentication-rate:{client-id=producer-1}              : 0.000
    producer-metrics:successful-authentication-total:{client-id=producer-1}             : 0.000
    producer-metrics:successful-reauthentication-rate:{client-id=producer-1}            : 0.000
    producer-metrics:successful-reauthentication-total:{client-id=producer-1}           : 0.000
    producer-metrics:waiting-threads:{client-id=producer-1}                             : 0.000
    producer-node-metrics:incoming-byte-rate:{client-id=producer-1, node-id=node--1}    : 13.231
    producer-node-metrics:incoming-byte-rate:{client-id=producer-1, node-id=node-0}     : 24.905
    producer-node-metrics:incoming-byte-total:{client-id=producer-1, node-id=node--1}   : 518.000
    producer-node-metrics:incoming-byte-total:{client-id=producer-1, node-id=node-0}    : 973.000
    producer-node-metrics:outgoing-byte-rate:{client-id=producer-1, node-id=node--1}    : 2.375
    producer-node-metrics:outgoing-byte-rate:{client-id=producer-1, node-id=node-0}     : 57.285
    producer-node-metrics:outgoing-byte-total:{client-id=producer-1, node-id=node--1}   : 93.000
    producer-node-metrics:outgoing-byte-total:{client-id=producer-1, node-id=node-0}    : 2238.000
    producer-node-metrics:request-latency-avg:{client-id=producer-1, node-id=node--1}   : NaN
    producer-node-metrics:request-latency-avg:{client-id=producer-1, node-id=node-0}    : 14.444
    producer-node-metrics:request-latency-max:{client-id=producer-1, node-id=node--1}   : NaN
    producer-node-metrics:request-latency-max:{client-id=producer-1, node-id=node-0}    : 26.000
    producer-node-metrics:request-rate:{client-id=producer-1, node-id=node--1}          : 0.051
    producer-node-metrics:request-rate:{client-id=producer-1, node-id=node-0}           : 0.256
    producer-node-metrics:request-size-avg:{client-id=producer-1, node-id=node--1}      : 46.500
    producer-node-metrics:request-size-avg:{client-id=producer-1, node-id=node-0}       : 223.800
    producer-node-metrics:request-size-max:{client-id=producer-1, node-id=node--1}      : 50.000
    producer-node-metrics:request-size-max:{client-id=producer-1, node-id=node-0}       : 340.000
    producer-node-metrics:request-total:{client-id=producer-1, node-id=node--1}         : 2.000
    producer-node-metrics:request-total:{client-id=producer-1, node-id=node-0}          : 10.000
    producer-node-metrics:response-rate:{client-id=producer-1, node-id=node--1}         : 0.051
    producer-node-metrics:response-rate:{client-id=producer-1, node-id=node-0}          : 0.256
    producer-node-metrics:response-total:{client-id=producer-1, node-id=node--1}        : 2.000
    producer-node-metrics:response-total:{client-id=producer-1, node-id=node-0}         : 10.000
    producer-topic-metrics:byte-rate:{client-id=producer-1, topic=hello.kafka}          : 41.962
    producer-topic-metrics:byte-total:{client-id=producer-1, topic=hello.kafka}         : 1639.000
    producer-topic-metrics:compression-rate:{client-id=producer-1, topic=hello.kafka}   : 1.000
    producer-topic-metrics:record-error-rate:{client-id=producer-1, topic=hello.kafka}  : 0.000
    producer-topic-metrics:record-error-total:{client-id=producer-1, topic=hello.kafka} : 0.000
    producer-topic-metrics:record-retry-rate:{client-id=producer-1, topic=hello.kafka}  : 0.000
    producer-topic-metrics:record-retry-total:{client-id=producer-1, topic=hello.kafka} : 0.000
    producer-topic-metrics:record-send-rate:{client-id=producer-1, topic=hello.kafka}   : 0.256
    producer-topic-metrics:record-send-total:{client-id=producer-1, topic=hello.kafka}  : 10.000
    ```
    

### **kafka-consumer-perf-test.sh**

카프카 컨슈머로 퍼포먼스를 측정할 때 사용된다.
카프카 브로커와 컨슈머(여기서는 해당 스크립트를 돌리는 호스트)간의 네트워크를 체크할 때 사용할 수 있다.

```bash
$ bin/kafka-consumer-perf-test.sh \
	--bootstrap-server my-kafka:9092 \
	--topic hello-kafka \
	--messages 10 \
	--show-detailed-stats

time, threadId, data.consumed.in.MB, MB.sec, data.consumed.in.nMsg, nMsg.sec, rebalance.time.ms, fetch.time.ms, fetch.MB.sec, fetch.nMsg.sec
[2022-12-31 19:10:27,439] WARN [Consumer clientId=consumer-perf-consumer-64485-1, groupId=perf-consumer-64485] Error while fetching metadata with correlation id 2 : {hello-kafka=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
WARNING: Exiting before consuming the expected number of messages: timeout (10000 ms) exceeded. You can use the --timeout option to increase the timeout.
```

- 특정 클라이언트 환경에서 테스트 해볼 수 있다.

### **kafka-reassign-partitions.sh**

리더 파티션이 특정 브로커에 몰렸을 경우(hot spot) 이때 리더 파티션과 팔로워 파티션을 분산시킬때 사용된다.

- kafka-reassign-partitions.sh를 사용하면 리더 파티션과 팔로워 파티션이 위치를 변경할 수 있다.
- 카프카 브로커에는 auto.leader.rebalance.enable 옵션이 있는데 이 옵션의 기본값은 true로써 클러스터 단위에서 리더 파티션을 자동 리밸런싱하도록 도와준다.
- 브로커의 백그라운드 스레드가 일정한 간격으로 리더의 위치를 파악하고 필요시 리더 리밸런싱을 통해 리더의 위치가 알맞게 배분된다.

### **kafka-delete-record.sh**

지정한 offset 까지 레코드를 지우는 명령이다.

```bash
# delete.json
$ cat delete.json
{
	"partitions": [
		{
			"topic": "hello.kafka", "partition": 0, "offset": 5
		}
	],
	"version": 1
}

# delete.json을 지정해서 delete 커맨드 실행
$ bin/kafka-delete-record.sh \
	--bootstrap-server my-kafka:9092 \
	--offset-json-file delete.json

Executing records delete operation
Records delete operation completed:
partition: hello-kafka-0   low_watermark: 5
```

### **kafka-dump-log.sh**

세그먼트 단위로 상세 로그를 확인하는 명령이다. 일반적인 상황에서는 잘 쓰이지는 않지만 확인이 필요할 경우 활용할 수 있다.

```bash
$ bin/kafka-dump-log.sh \
	--files data/hello.kafka-0/00000000000000000000.log \
	--deep-iteration
```

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