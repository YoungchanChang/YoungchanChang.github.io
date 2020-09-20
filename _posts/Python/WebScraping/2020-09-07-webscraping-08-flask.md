---
layout: post
title: 웹스크래핑08. flask개념과 설치
category: webscraping
tags: [python, webscraping]
comments: python
---

# flask

### flask란?

- 파이썬용 서버

### flask를 쓰는 이유는?

- Django보다 가볍다. 가볍게 실행시키기에 좋다.

### flask 실행시켜보기

- 1.flask 설치하기

```
$ pip install Flask
```

- 2.flask 구동하기
- 데코레이터 : 함수에 추가적인 기능을 주입하는데 사용
- @app.route("/")는 서버에서 해당 경로로 요청이 오면 바로 아래 함수를 실행한다는 데코레이터
- 메소드여야함. 데코레이터는 바로 아래에 있는 함수만 본다.

```python
from flask import Flask
app = Flask("SuperScrapper")

@app.route("/")
def home():
    return "Hello! Welcome to mi casa!"

@app.route("/route")
def potato():
    return "Contact me!"

app.run(host="127.0.0.1", port=5001)
```

### 추가로 알아야 할 사항

- 서버의 구성중 MVC모델이 있다. Model(데이터베이스) View(결과 화면) Controller(입력과 처리)의 의미이다.

- 위의 예시는 Controller(입력과 처리)의 동작을 보여준다.

# 참고

[flask 설치](https://flask.palletsprojects.com/en/1.1.x/installation/)

[데코레이터](https://flask-docs-kr.readthedocs.io/ko/latest/patterns/viewdecorators.html)

[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)
