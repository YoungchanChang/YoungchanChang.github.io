---
layout: post
title: flask에서 엘라스틱서치 인덱스 셋팅변경
category: python
tags: [python, 쓰기]
comments: true
---


# 엘라스틱 서버에서 requests요청하기

- `PUT localhost:9200/index_name/_settings`으로 넣는다.

```
{
    "index": {
      "analysis":{
         "analyzer":{
            "nori_analyzer":{
               "type":"custom",
               "tokenizer":"nori_tokenizer"
            }
         }
      }
    }
}
```

# 매핑 변경하기

- `PUT /my-index-000001/_mapping`으로 넣는다.

```
{
  "properties": {
    "email": {
      "type": "keyword"
    }
  }
}
```


# 참조

[셋팅 변경](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-update-settings.html)

[매핑 변경](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-put-mapping.html)