---
layout: post
title: setting설정하기
category: python
tags: [python, 쓰기]
comments: true
---

# 인덱스 setting custom하기

- 셋팅에서 인덱스의 환경설정을 할 수 있고, 매핑에서 인덱스 구조를 정의할 수 있다.

- 인덱스의 환경설정에서는 **분석기와 유사도**를 설정할 수 있다.

- 분석기는 아날라이저, 필터로 이루어진다. **아날라이저 안에서 필터를 설정**하면 된다.

- 유사도에서는 type, k1, b, discount_overlaps를 설정할 수 있다.

```json
PUT [http://localhost:9200/korean]
{
    "settings": {
        "index": {
            //분석기 구성요소 : 아날라이저, 필터
            "analysis": {
                "analyzer": {
                    "nori_analyzer": {
                        "type": "custom",
                        "tokenizer": "nori_tokenizer",
                        //필터에 동의어 말고도 숫자 처리도 있다.
                        "filter": [
                            "part_of_speech_stop_sp",
                            "nori_number"
                        ]
                    },
                    "nori_custom_analyzer": {
                        "type": "custom",
                        "tokenizer": "nori_tokenizer",
                        "filter": "nori_synonym_filter"
                    }
                },
                //필터 선택권 : 동의어, 품사분석기
                "filter": {
                    "nori_synonym_filter": {
                        "type": "synonym",
                        "synonyms_path": "analysis/synonym.txt"
                    },
                    "part_of_speech_stop_sp": {
                        "type": "nori_part_of_speech",
                        "stoptags": []
                    }
                }
            },
            // 유사도 측정
            "similarity": {
                "my_custom_similarity": {
                    "type": "BM25",
                    "k1": 1.2,
                    "b": 0.75,
                    "discount_overlaps": false
                }
            }
        }
    },
    "mappings": {
        "properties": {
            // 속성 선택 : 텍스트냐 term이냐
            "sentence": {
                "type": "text",
                "analyzer": "nori_analyzer",
                "search_analyzer": "nori_custom_analyzer",
                "similarity": "my_custom_similarity"
            },
            "content": {
                "type": "text",
                "analyzer": "nori_analyzer",
                "search_analyzer": "nori_custom_analyzer",
                "similarity": "my_custom_similarity"
            }
        }
    }
}
```


# 셋팅 바꾸기

- 인덱스 클로스한다.

- 셋팅부분의 경로에 PUT으로 인덱스를 바꾼다.

- 인덱스 오픈한다.

```json
- PUT localhost:9200/korean/_settings
{
    "index": {
      "analysis":{
         "analyzer":{
            "nori_analyzer":{
               "type":"custom",
               "tokenizer":"nori_tokenizer"
            },
            "nori_bokji_analyzer":{
                "type":"custom",
                "tokenizer":"nori_tokenizer",
                "filter":"nori_synonym_filter"
            }
         },
         "filter":{
             "nori_synonym_filter" : {
                 "type" : "synonym",
                 "synonyms_path" : "analysis/synonym.txt"
             }
         }
      }
   }
}

```

# 매핑 바꾸기

- 인덱스 클로스한다.

- 매핑부분의 경로에 PUT으로 인덱스를 바꾼다.

- 인덱스 오픈한다.

```json
- PUT localhost:9200/korean/_mapping
{
         "properties":{
            "user_type": {
                "type":"keyword"
            },
            "large_category": {
                "type":"text",
                "analyzer":"nori_analyzer",
                "search_analyzer":"nori_bokji_analyzer"
            }
      }
}
```

# 리인덱스하기

- 인덱스를 수정할 때 쓰인다.

```json
curl -H 'Content-Type: application/json' -XPOST http://my-elasticsearch-host:9200/_reindex -d 
{
  "source": {
    "index": "old-index-name"
  },
  "dest": {
      "index": "new-index-name"
  }
}
```

[Reindex](https://findstar.pe.kr/2018/07/07/elasticsearch-reindex/)