---
title: Elasticsearch 재인덱싱
categories: elasticsearch
---

# Elasticsearch 기본 내용 정리
  
1. 새 인덱스 생성
    
    ```json
    PUT books_2
    {
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
            "type": "date",
            "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
          },
          "title_second": {
            "type": "text"
          }
        }
      }
    }
    ```
    
2. 기존 인덱스를 소스로 하는 재 인덱싱을 진행
    
    ```json
    POST _reindex?wait_for_completion=false // wait_for_completion 옵션을 설정해서 비동기로 실행
    {
      "source": {
        "index": "books"
      },
      "dest": {
        "index": "books_2"
      }
    }
    ```
    
3. 재 인덱싱 진행시 얻은 task 번호를 통해 현재 진행상태를 확인할 수 있음
    
    ```json
    GET _tasks/q8QhrcEJQPWRI-qBfeSeTw:1446977775
    ```
    
4. Alias 교체 작업
    
    ```json
    POST _aliases
    {
      "actions": [
    		{
          "remove": {
            "index": "books_1",
            "alias": "alias_books"
          }
        },
        {
          "add": {
            "index": "books_2",
            "alias": "alias_books",
    				"is_write_index": true # alias 에서 write 는 단 1개의 인덱스만 가능하다.
          }
        }
      ]
    }
    ```
