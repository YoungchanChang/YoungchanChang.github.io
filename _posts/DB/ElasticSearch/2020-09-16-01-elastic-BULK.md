---
layout: post
title: 엘라스틱서치 버크
category: python
tags: [python, 쓰기]
comments: true
---

# 버크로 저장하기

- 데이터가 많을 때 한꺼번에 저장할 때 사용한다.

`curl -XPOST http://localhost:9200/bulk?pretty -data-binary @classes.json`

### MAPPINDG - schema와 동일하다.

- mapping 없이도 데이터를 넣을 수 있다. 그러나 document에 date를 넣을 때, mapping이 없다면 날짜일지 모르니깐 문자열로 저장할 수 있다. 숫자인지 문자인지 구분 안 될 때 문자열로 넣을 수 있다. 잘못 지정된 type은 kibana에서 시각화할 때 되지 않는다. 평균, 최고값을 내기 힘들다. 데이터를 관리할 때는 mapping을 먼저 추가하면 된다.

```
{
"class" :{
        "properties : {
            "title" : {"type" : "string"},
            "professor" : {"type" : "string"},
            "major" : {"type" : "string"},
            "semester" : {"type" : "string"},
            "student_count" : {"type" : "string"},
            "submit_date" : {"type" : "date", "format" : "yyyy-MM-dd"},
            "school_location" : {"type" : "geo_point"}
        }
    }
}
```
- `curl -XPUT 'http://localhost:9200/classes'`를 하면 mapping이 비어있다.

### mapping

- `curl XPUT 'http://localhost:9200/classes/class/_mapping' -d @classesRating_mapping.json`에 매핑을 추가하면 같은 명령어를 쳤을 때 속성이 나온다.

- 추가한 mapping은 `localhost:9200/product_list1/_mapping`로 검색할 수 있다.

- type이 정해졌으므로 aggregation이나 시각화를 할 때 type을 활용할 수 있다.

### 데이터 조회하기

- `curl -XPOST 'localhost:9200/_bulk' --data-binary @simple_basketball.json`로 데이터 집어넣기

- `curl -XGET localhost:9200/basketball/record/_search?pretty`하면 결과값으로 2개의 결과가 나온다.

- `curl -XGET localhost:9200/basketball/record/_search?q=points:30&pretty`하면 point 30의 결과가 조회된다.

- `curl -XGET localhost:9200/basketball/record/_search -d { "query" : {"term" : {"points" : 30}}}`으로 데이터를 통해 결과를 조회할 수 있다.