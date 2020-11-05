---
layout: post
title: 엘라스틱서치 tokenizer
category: elasticsearch
tags: [elasticsearch]
comments: true
---

# 인덱스 생성

- `PUT domain`으로 index를 생성한다.

- `PUT domain/index/type/id`를 통해서 document를 저장한다. mapping과 setting이 자동으로 생성된다.

- `GET /index`를 하면 셋팅이 확인이 가능하다.

- 같은 도메인으로 쓰면 덮어쓰기도 가능하다.

# 검색하기

- 알아야 할 것 : 쿼리로 검색하기

- 부분으로 검색하기 제대로하기

- 전체 검색

```
GET localhost:9200/customer/_search
{
  "query": { "match_all": {} }
}
```
- 조건 검색

```
GET localhost:9200/customer/_search
{
"query": { "match": { "school" : "서울에서" } }
}
```


```
{
    "customer": {
        "aliases": {},
        "mappings": {
            "properties": {
                "ages": {
                    "type": "text",
                    "fields": {
                        "keyword": {
                            "type": "keyword",
                            "ignore_above": 256
                        }
                    }
                }
            }
        },
        "settings": {
            "index": {
                "creation_date": "1600309193411",
                "number_of_shards": "1",
                "number_of_replicas": "1",
                "uuid": "OSXe6cciT8SKKnpkfCSHdg",
                "version": {
                    "created": "7090199"
                },
                "provided_name": "customer"
            }
        }
    }
}
```

### 한글 검색을 위해 설치하기

- custom 분석기 사용

### 

- 에러코드 : "Can't update non dynamic settings [[index.analysis.tokenizer]] for open indices [[customer/OSXe6cciT8SKKnpkfCSHdg]]"

- close하고 한다.

# 참조

[엘라스틱 저장 구조](https://www.slideshare.net/kjmorc/ss-80803233)

[토크나이저 설명](https://esbook.kimjmin.net/06-text-analysis/6.3-analyzer-1/6.4.1-_termvectors-api)

[노리 설정](https://www.lesstif.com/dbms/elastic-search-nori-80248960.html)

[토크나이저 설정하기](https://www.lesstif.com/dbms/elastic-search-nori-80248960.html)