---
layout: post
title: 엘라스틱서치 Analyize results with aggregations
category: elasticsearch
tags: [elasticsearch]
comments: true
---

# Aggregations(집합)을 이용해서 검색하기

- Aggregtaions를 이용해서 검색 결과에 대한 meta-information를 얻을 수 있다. "텍사스에 얼마나 많은 부지가 있는가?"나 "테네시의 평균은"등을 검색할 수 있다.

- 여기서 부지 자체를 검색어로 쓰지 않고 **부지들을 묶어서 어떤 결과를 검색**할 수 있는 것을 Aggrgations라고 한다.

- 아래 코드는 state가 키워드인 열(field)로 묶은 결과를 보여준다.

```
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      }
    }
  }
}
```

- 검색 결과를 중첩해서 보여줄 수도 있다. state열로 묶은 다음에, balance열로 평균을 보여줄 수 있다.

```
GET /bank/_search
{
  "size": 0,
  "aggs": {
    "group_by_state": {
      "terms": {
        "field": "state.keyword"
      },
      "aggs": {
        "average_balance": {
          "avg": {
            "field": "balance"
          }
        }
      }
    }
  }
}
```


- 기본적인 bucketing과 집합기능에 더해 **날짜, IP주소, 지역정보**같은 정보를 집합으로 이용할 수 있다.

### Aggregation

- 집합의 개념 : 다른 클래스를 묶는 것을 말한다. 묶는 객체 자체가 없어지지 않는 한 없어지지 않아야 한다. 유의어 : `group`

- MySQL에서 행들의 집합 수 만큼 결과가 반환된다. GROUP BY 뒤에 컬럼을 추가하면 된다.


# 참고문서

[엘라스틱 서치 aggregations](https://esbook.kimjmin.net/08-aggregations)

[Aggregation](http://dos.iitm.ac.in/OOSD_Material/Basic%20Concepts/Basic%20Concepts%20Of%20OO/aggregation.htm)

[RDBMS와 인덱스 설치](https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84)

[Aggregation 집합함수](https://www.slideshare.net/topcredu/1-75765533)