---
title: Elasticsearch 기본 내용 정리
categories: Elasticsearch
---

# Elasticsearch 기본 내용 정리
  
## Node roles

- 노드 역할 종류
    - master(m)
    - data(d)
    - data_content(s)
    - data_hot(h)
    - data_warm(w)
    - data_cold(c)
    - data_frozen(f)
    - ingest(i)
    - remote_cluster_client(r)
    - ml(l)
    - transform(t)
    - voting_only(v)

## API

- 노드 정보 확인
    - 노드 정보 및 클러스터 구성 확인
        - `http://node:9200/_cat/nodes`
- Format
    - api 호출 결과 포맷
        - `?format=json&pretty`
        - `?v`
- Document
    - 입력
        - PUT
            - http://node:9200/_doc/{doc_id}
                - 없으면 생성
                - 있으면 수정
            - http://node:9200/_create/{doc_id}
    - 수정
        - POST
            - http://node:9200/_doc/{doc_id}
                - doc_id 를 입력하지 않을 시 자동으로 임의의 doc_id 가 생성된다.
            - http://node:9200/_update/{doc_id}
                - _update api 로 특정 필드만을 수정할때 doc 이라는 지정자를 사용해서 적용할 수 있다.
                
                ```json
                "doc": {
                	"messge": "안녕하세요"
                }
                ```
                
    - 삭제
        - DELETE
            - http://node:9200/_doc/{doc_id}
- Index
    - 매핑정보 수정
        - 필드 추가 : 중복 필드명 불가
        - PUT `http://node/books/_mapping`
        
        ```json
        "properties": {
        	"<추가할 필드명>": {
        		"type": "<필드 타입>",
        		...<필드 설정>
        	}	
        }
        ```
        
        - 필드 삭제 : 불가
        - 필드 수정 : 불가
        - 필드의 삭제 및 수정이 필요할 경우
        - 필드의 변경이 필요한 경우 인덱스를 새로 정의하고 기존 인덱스의 값을 새 인덱스에 모두 재색인 해야한다.
    - 인덱스 삭제
        - DELETE books

[재인덱싱](https://www.notion.so/e392fda019244cba9307ab8b89335765)

## Alias

- 인덱스에 대한 별칭
    - alias 조회
        - http://node/_alias
    - 생성 및 추가
        - http://node:9200/_aliases
        
        ```json
        {
        	"actions": [
        		"add" : {
        			"index": "book1",
        			"alias": "books",
              // optional
        			// 기본적으로 하나의 alias에 인덱스가 2개 이상일 경우 오류가 발생하며 인덱싱 되지 않는다.
        			// 하나의 alias 에 여러 index 를 지정하고 데이터를 저장하고 싶을 경우 특정 1개의 인덱스에 아래 옵션을 지정해줘야 한다.
        			"is_write_index": true
        		}
        	]
        }
        ```
        
    - 삭제
        - http://node/_aliases
        
        ```json
        {
        	"actions": {
        		"remove": {
        			"index": "book1",
        			"alias": "books"
        		}
        	}
        }
        ```
        
    - 1개의 Alias에 2개 이상의 index가 설정되어 있을 경우 1개의 Alias 당 정확히 1개의 index만 write 가능 (index/update) index로 설정할 수 있다.
    - 2개 이상의 index가 Alias 와 연결되어 있는 경우, 어느 하나의 Index에 명시적으로 is_write_index가 설정되어 있어야 데이터 입력이 정상적으로 되며, 그렇지 않을 경우 오류가 발생한다.

## Clustering

- 클러스터링 자동 구성
    - 아무런 설정이 되어있지 않을 경우 같은 네트워크 대역의 여러 노드들은 같은 이름의 클러스터로 클러스터링 된다. (기본 클러스터명 : elasticsearch)

<aside>
💡 하지만 자동 구성보다는 명시적인 클러스터링 구성 방식을 권고한다.

</aside>

## Schema less, Dynamic mapping

- Schema less
    - 엘라스틱 서치는 관계형 DB와의 큰 차이점들 중 하나인 스키마리스 기능을 제공한다.
    - 문서를 색인할 때 해당 인덱스가 없으면 문서의 필드 정보를 참고해 자동으로 인덱스를 생성한 후 문서를 색인한다.
    - 자동으로 생성된 인덱스는 text 와 keyword 를 동시에 매핑하게 된다. 필요없는 타입까지 지정될 수 있으므로 리소스 낭비의 여지가 생기게 된다.
    - 스키마리스 기능은 리소스 낭비를 유발하며, 프로그래머의 실수로 잘못된 매핑이 생성되면 시스템의 안정성을 해칠 수 있으므로 가급적 스키마리스 기능은 사용하지 말아야한다.
    
    <aside>
    💡 스키마리스 설정
    
    [ elasticsearch.yml ]
    action.auto_create_index: false #스키마리스 기능 off
    
    </aside>
    
- Dynamic mapping / 동적 매핑
    - 엘라스틱 서치에는 존재하지 않는 인덱스를 자동으로 생성하는 스키마리스 이외에도 존재하지 않는 필드를 자동으로 생성하는 동적 매핑 기능도 있다.
    - 스키마리스와 동일하게 자동으로 생성된 필드의 매핑정보가 text 와 keyword 두 가지를 제공하도록 설정된다.
    - 만약 실수로 인덱스 생성 과정에서 특정 필드를 빠뜨리고 색인을 생성했다면 추후에 자동으로 해당 필드의 매핑 정보가 생성되기 때문에 색인을 할 때 문제를 알아차리기 어려울 수 있다.
    
    <aside>
    💡 동적 매핑 설정
    
    - 동적 매핑을 사용하지 않으려면 인덱스 생성시에 mapping 정보의 dynamic 속성을 “strict” 로 설정하면 된다.
    
    ```json
    PUT /books
    {
      "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
      },
      "mappings": {
        "properties": {
          "title": {
            "type": "text"
          },
          "titleEn": {
            "type": "text"
          },
          "writer": {
            "type": "text"
          },
          "productDate": {
            "type": "date"
          }
        },
        "dynamic": "strict"
      }
    }
    ```
    
    </aside>
    
    - dynamic 속성 종류
        - true : 새로운 필드는 매핑에 추가된다. (기본값)
        - runtime : 새로운 필드는 런타임 필드로 매핑에 추가된다. 이러한 필드는 인덱싱 되지 않으며 쿼리시 _source 에서 로드된다.
        - false : 새로운 필드는 무시된다. 이러한 필드는 인덱싱되거나 검색되지 않지만 반환된 히트의 _source 필드에 계속 표시됩니다. 이러한 필드는 매핑에 추가되지 않으며 새 필드를 명시적으로 추가해야 합니다.
        - strict : 새로운 필드가 감지되면, 예외를 던진다. 새로운 필드는 명시적으로 추가해야한다.

## Aggregation

- Elastic search는 집계를 위한 기능을 제공한다.
- query 결과에서 집계가 이루어 진다.
- query 문과 같은 수준에 지정자 aggregations or aggs 를 명시한다.

- Metrics Aggregation
    - 필드의 값으로 계산을 하는 aggregation 이다.
        - min, max, sum, avg, stat(min, max, sum, avg 모두)
        - cardinality : 필드값의 종류 갯수
        - percentiles : 지정 백분위의 값들을 가져온다
        - percentile_ranks : 값으로 해당 백분위를 가져온다
- Bucket Aggregation
    - 범위나 keyword 값 등을 가지고 도큐먼트들을 그룹화 하는 aggregation 이다.
        - range : ‘to’, ‘from’ 을 조합하여 해당 범위의 값을 가진 도큐먼트의 갯수를 집계
        - histogram : interval 옵션을 이용해서 주어진 간격 크기대로 버킷을 구분하여 도큐면트의 갯수를 집계
        - terms : keyword 필드의 문자열 별로 버킷을 나누어 집계. field 옵션으로 필드를 지정한다.
        - field 외에도 가져올 수 있는 버킷의 갯수를 지정하는 size 옵션이 있으며 기본값은 10이다.

## Query

- shoud
    - **minimum_should_match** : should 조건에 일치여부를 결정하는 옵션
        - 기본값은 1이다.
        - 0 이라면 should 아무 조건에 해당하지 않더라도 true 가 된다.
        - 1 이상일 경우 해당 조건 갯수 이상 만족할 경우 true 가 된다.
        - **must 와 함께 사용될 경우 기본값은 0으로 지정된다.**
- hit total value
    - elasticsearch 7 이상 부터는 결과 갯수가 10000개 이상일 때, 정확한 갯수를 얻기 위해서는 `"track_total_hits"` 옵션을 true 로 해서 쿼리해야한다.
    - track_total_hits 옵션을 true 지정하지 않으면 결과 에서 `"relation" : "gte”` 로 10000 개보다 많다는 상태값만 알려준다.
        
        ```json
        GET alias_deartail_products/_search
        {
          "from": 0,
          "size": 1,
        	"track_total_hits": true,
          "query": {
            "bool": {
              "filter": [
                {
                  "range": {
                    "documentedAt": {
                      "gte": 1659290500000
                    }
                  }
                }
              ]
            }
          }
        }
        ```