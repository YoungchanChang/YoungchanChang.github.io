---
layout: post
title: 웹스크래핑12. FasterScrapper
category: python
tags: [python, webscraping]
comments: python
---

# FasterScrapper

- 크롤링한 정보를 데이터베이스(여기서는 배열)에 저장한 뒤 출력하는 과정

- 매 번 크롤링을 요청하면 속도가 느려짐

### 과정 상세

- 크롤링에서 가져온 정보를 객체에 저장한다. 크롤링 요청 단어에 맞춰서 저장한다.

- 클라이언트가 단어를 요청했을 시 DB에 자료가 있다면 해당 자료를 출력하고, 없다면 크롤링한 후 출력한다.

- 사용자에게 결과 출력하는 코드

```html
    <h1>Search Search</h1>
    <h3>Found {{resultsNumber}} results for : {{SearchingBy}}</h3>
```