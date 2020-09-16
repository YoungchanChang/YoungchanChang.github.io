---
layout: post
title: 엘라스틱서치란
category: python
tags: [python, 쓰기]
comments: true
---

# 일라스틱 서치란?

- 데이터 검색을 쉽고 빠르게 하는 것으로 빅데이터에 자주 쓰인다.

# 일라스틱 서치 RDBMS 비교

### 자료 저장 방식

- RDBMS는 데이터를 **테이블 형태**로 저장한다. 열을 기준으로 인덱스를 만든다. **책의 맨 앞에 있는 제목 리스트**와 같다.

- 검색엔진에서는 **inverted index구조**로 저장한다. RDBMS와는 반대 구조이다. 텍스트를 다 뜯어서 검색어 사전을 만든다. **책의 맨 뒤에 있는 페이지를 가리키는 키워드**와 같다.

### 일라스틱 서치 자료구조

- Elaistic자료구조는 해쉬테이블과 같아서 Big-O(1)의 속도를 갖는 반면, Realtional db자료구조는 Big-O(n)의 속도를 갖게 된다. search관점에서는 매우 빠르다.

- Index안에 type이 있고 그 안에 여러 document들이 있다. document들은 **같은 property**들을 갖고 있다.

### 자료의 CRUD

- 일라스틱 서치는 REST API로 자료를 CRUD(Create, Read, Update, Delete)한다.

- GET - READ / PUT - UPDATE / POST - CREATE / DELETE - DELETE


### 참고

인덱스와 RDBMS

인덱스(Index) | 데이터베이스(Database)
샤드(Shard) | 파티션(Partition)
타입(Type) | 테이블(Table)
문서(Document) | 행(Row)
필드(Field) | 열(Column)
매핑(Mapping) | 스키마(Schema)
Query DSL | SQL


###

# 참고문서

[RDBMS 비교2](https://victorydntmd.tistory.com/308)

[RDBMS 슬라이드](https://www.slideshare.net/kjmorc/ss-80803233)

[RDBMS 비교](https://velog.io/@jakeseo_me/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2-DB%EB%A7%8C-%EC%9E%88%EC%9C%BC%EB%A9%B4-%EB%90%98%EB%8A%94%EB%8D%B0-%EC%99%9C-%EA%B5%B3%EC%9D%B4-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84)
