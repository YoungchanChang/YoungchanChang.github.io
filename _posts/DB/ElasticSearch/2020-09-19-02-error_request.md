---
layout: post
title: flask에서 엘라스틱서치로 자료 요청하기
category: python
tags: [python, 쓰기]
comments: true
---


# 엘라스틱 서버에서 requests요청하기

- 엘라스틱 서치에서 requests를 import해야함. request가 아닌 `requests`임

```
import requests
```

# 파이썬에서 json추출하기

- 파이썬에서 객체의 필드는 **''싱글 쿼트**로 묶지만, JSON에서는 **""더블 쿼트**로 묶는다.

- 진짜 중요한 사실이다. csv파일을 json으로 바꿀 때도, requests요청을 할 때에도 형식을 바꿔줘야한다.


# 객체를 json으로 바꾸는 방법

- json으로 바꾸는 방법은 2가지가 있따. jsonify()와 json.dump()가 있다.

- json.dumps()는 객체를 json형식으로 직렬화해준다. json_encoder를 쓴다.

- jsonify()는 json.dump()를 감싸면서 몇가지 기능을 추가한 것이다. dumps()에 나온 결과를 application/json mimetype형식으로 바꿔준다. 인자값을 배열형태로 바꿔준다.

# json을 객체로 바꾸는 방법

- json.loads(r.text)

# 에러상황

- 에러코드 : Python Requests - No connection adapters

- 원인 : 앞에 http를 안 붙임.

- 해결책 : `'http://192.168.1.61:8080/api/call'`형식으로 보냄


# 참조

[엘라스틱 POST](https://stackoverflow.com/questions/9733638/post-json-using-python-requests)

[No connection adapters](https://stackoverflow.com/questions/15115328/python-requests-no-connection-adapters)

[파이썬 JSON추출](https://hashcode.co.kr/questions/8852/%ED%8C%8C%EC%9D%B4%EC%8D%AC-json-%ED%8A%B9%EC%A0%95%EA%B0%92-%EC%B6%94%EC%B6%9C)

[jsonify와 json.dump의 차이](https://velog.io/@matisse/flask-jsonify-%EC%99%80-json.dumps%EC%9D%98-%EC%B0%A8%EC%9D%B4)

[flask jsonify 공식문서](https://flask.palletsprojects.com/en/1.1.x/api/)