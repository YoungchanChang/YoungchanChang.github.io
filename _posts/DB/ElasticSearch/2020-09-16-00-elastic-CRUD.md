---
layout: post
title: 엘라스틱서치 인덱스, 도큐먼트 다루기
category: elasticsearch
tags: [elasticsearch]
comments: true
---

# 인덱스 생성

### 인덱스 확인

- 1.GET INDEX를 통해 인덱스가 있는지 확인한다.

`curl -XGET http://localhost:9200/classes`

- 결과값을 깔끔하게 보고싶다면 ?pretty를 param으로 넣는다.

`curl -XGET http://localhost:9200/classes?pretty`

### 인덱스 생성

- PUT을 통해 인덱스 생성

`curl -XPUT http://localhost:9200/classes`

### 인덱스 삭제

- DELETE을 통해 인덱스 생성

`curl -XDELETE http://localhost:9200/classes`


# Document

### document 생성

- DOCUMENT는 index가 없어도 생성이 가능하다. **인덱스와 타입명**을 기재하면 된다

`curl -XPOST https://localhost:9200/classes/class/1/ -d '{"title" : "Algorithm", "professor" : "Jhon" }`

### 파일에 있는 document 저장

- d @를 쓰고 데이터 이름을 써주면 된다.

`curl -XPOST http://localhost:9200/classes/class/1/ -d @oneclass.json`

### document 조회

`curl -XGET http://localhost:9200/classes/class/1?prtty`

### document에 field추가 (UPDATE)

- `class/type/id/_update`로 데이터를 넣는다.

`curl -XPOST http://localhost:9200/classes/class/1/_update -d '{"doc" : {"unit" : 1 }}'`

- script를 사용해서 값을 바꿀 수 있다.

`curl -XPOST http://localhost:9200/classes/class/1/_update -d '{"script" : {"ctx._source.unit += 5" }}'`

# 참고문서

[RDBMS 비교2](https://victorydntmd.tistory.com/308)

[RDBMS 슬라이드](https://www.slideshare.net/kjmorc/ss-80803233)

[RDBMS 비교](https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84)
