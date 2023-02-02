---
title: Kafka 스트림즈 DSL Queryable store
categories: Kafka
---

카프카 스트림즈에서 KTable은 카프카 토픽의 데이터를 로컬의 rocksDB에 Meterialized View로 만들어 두고 사용하기 때문에 레코드의 메세지 키, 메세지 값을 기반으로 keyValueStore로 사용할 수 있다.

특정 토픽을 KTable로 사용하고 ReadOnlyKeyValueStore로 뷰를 가져오면 메세지 키를 기반으로 토픽 데이터를 조회할 수 있게 된다. 

마치 카프카를 사용하여 로컬 캐시를 구현한것과 유사하다고 볼 수 있다.

- code
    
    ```kotlin
    val builder = StreamsBuilder()
    val addressTable = builder.table(ADDRESS_TABLE, Meterialized.as(ADDRESS_TABLE))
    
    val keyValueStore = streams.store(
    	StoreQueryParameters.fromNameAndType(
    		ADDRESS_TABLE, QueryableStoreTypes.keyValueStore()
    	)
    )
    
    val address: KeyValueIterator = keyValueStore.all()
    address.forEachRemaining { keyValue ->
    	log.info { keyValue }
    }
    ```