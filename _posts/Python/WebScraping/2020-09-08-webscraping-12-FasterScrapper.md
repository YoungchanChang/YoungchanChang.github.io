---
layout: post
title: 웹스크래핑12. FasterScrapper
category: webscraping
tags: [python, webscraping]
comments: python
---

# FasterScrapper

### FasterScrapper란?

- 크롤링한 정보를 데이터베이스(여기서는 배열)에 저장한 뒤 출력하는 과정

### FasterScrapper을 하는 이유

- 매 번 크롤링을 요청하면 속도가 느려짐으로 크롤링 데이터를 DB에 저장해놓고 출력하면 속도가 향상될 수 있다.

### 과정 상세

- 1.크롤링에서 가져온 정보를 객체에 저장한다. 크롤링 요청 단어에 맞춰서 저장한다.

```python
    db = {}
    jobs = get_result(word)
    db[word] = jobs
```

- 2.클라이언트가 단어를 요청했을 시 DB에 자료가 있다면 해당 자료를 출력하고, 없다면 크롤링한 후 출력한다.

```python
    if word:
        word = word.lower()

        # db에 존재하는지 검색하기
        db_exist = db.get(word) # db[word] 이 두개의 차이는 무엇이지?
        if db_exist:
            jobs = db_exist

        # db에 값이 없을 경우 검색해서 저장
        else:            
            jobs = get_result(word)
            db[word] = jobs
```

- 3.렌더링시 결과값을 다르게 주기 위해 검색 결과 숫자를 출력한다.

```python
    return render_template("result.html",
                           SearchingBy=word,
                           resultsNumber=len(jobs))

```

- 4.사용자에게 결과 출력하는 코드는 아래와 같다.

```html
    <h1>Search Search</h1>
    <h3>Found [[resultsNumber}} results for : [[SearchingBy}}</h3>
```

### 추가로 알아야 할 사항

- DB는 라우트 밖에 있어야 한다. route가 얼마나 실행되던지 상관 없이 실행될 수 있다.


# 전체 코드

```python
from flask import Flask, render_template, request, redirect
from scrapper import get_result

app = Flask("SuperScrapper")


db = {}


@app.route("/report")
def reporting():
    # print(request.args)
    word = request.args.get('word')

    if word:
        word = word.lower()

        # db에 존재하는지 검색하기
        # db[word]처럼 존재하지 않는 키(nokey)로 값을 가져오려고 할 경우 db[word]는 **Key 오류를 발생**시키고 db.get(word)는 **None을 돌려준다**는 차이가 있다.

        is_exist = db.get(word)
        if is_exist:
            jobs = is_exist

        else:
            jobs = get_result(word)
            db[word] = jobs

    return render_template("searchingResult.html",
                           SearchingBy=word,
                           resultsNumber=len(jobs))


app.run(host="127.0.0.1", port=5000)

```
