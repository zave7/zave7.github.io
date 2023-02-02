---
title: Kafka 스트림즈 프로세서 API
categories: Kafka
---

# Streams Processor API

프로세서API는 스트림즈DSL 보다 투박한 코드를 가지지만 토폴로지를 기준으로 데이터를 처리한다는 관점에서는 동일한 역할을 한다. 

스트림즈DSL은 데이터 처리, 분기, 조인을 위한 다양한 메서드들을 제공하지만 추가적인 상세 로직의 구현이 필요하다면 프로세서 API를 활용할 수 있다.

프로세서 API에서는 스트림즈DSL에서 사용했던 KStream, KTable, GlobalKTable 개념이 없다는 점을 주의해야 한다.

다만, 스트림즈DSL과 프로세서API는 함께 구현하여 사용할 때는 활용할 수 있다.

프로세서 API를 구현하기 위해서는 `Processor` 또는 `Transformer` 인터페이스로 구현한 클래스가 필요하다.

Processor 인터페이스는 일정 로직이 이루어 진 뒤 다음 프로세서로 데이터가 넘어가지 않을 때 사용한다.

반면, Transformer 인터페이스는 일정 로직이 이루어진 뒤 다음 프로세서로 데이터를 넘길 때 사용한다.

- code
    - FilterProcessor
        
        ```kotlin
        internal class FilterProcessor : Processor<String, String> {
        	private lateinit var context: ProcessorContext
        
        	override fun init(context: ProcessorContext) { this.context = context }
        
        	override fun process(key: String, value: String) {
        		if(value.length > 5) {
        			context.forward(key, value)
        		}
        		context.commit()
        	}
        
        	override fun close() {}
        }
        ```
        
    - SimpleKafkaProcessor
        
        ```kotlin
        fun main() {
        	val topology = Topology()
        	topology
        		.addSource("Sourece", STREAM_LOG)
        		.addProcessor("Process", ::FilterProcessor, "Source")
        		.addSink("Sink", STREAM_LOG_FILTER, "Processor")
        
        	val streaming = KafkaStreams(topology, prors)
        	streaming.start()
        }
        ```