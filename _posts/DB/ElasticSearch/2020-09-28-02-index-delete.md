---
layout: post
title: TermVector
category: elasticsearch
tags: [elasticsearch]
comments: true
---

# 인덱스 생성, 삭제

- es.indices.create()임

# 에러 발생

- 에러 코드 : (ConnectionTimeout caused by - ReadTimeoutError(HTTPConnectionPool(host='localhost', port=9200): Read timed out. (read timeout=10))

- 여러 해결책을 찾았지만 실패. 그냥 엘라스틱서치 껏다 키니깐 됬음

# 참고

[인덱스 생성, 삭제](https://elasticsearch-py.readthedocs.io/en/master/api.html#indices)

[스택오버플로우](https://stackoverflow.com/questions/35134162/elasticsearch-how-to-delete-an-index-using-python)

[다른 경로 파일 읽기](https://brownbears.tistory.com/296)

[파일 읽기](https://m.blog.naver.com/PostView.nhn?blogId=damoen7&logNo=221432243063&proxyReferer=https:%2F%2Fwww.google.com%2F)