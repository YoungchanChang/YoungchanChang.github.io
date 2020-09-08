---
layout: post
title: 웹스크래핑03. 파이썬으로 HTML파일 내용 가져오기
category: python
tags: [python, webscraping]
comments: python
---

# 파이썬을 이용해서 웹페이지의 html내용을 가져오기

    - request 모듈을 활용

### 과제 진행 순서

1] [request 모듈 설치](https://github.com/psf/requests)

2] html내용을 가져오기. 결과값은 `<Response [200]>`임

3] 검색 결과에서 html 본문 내용 뽑아내기

### 과제 상세 진행

1] [request 모듈 설치](https://github.com/psf/requests)

```
$ python -m pip install requests
```

2] html내용을 가져오기. 결과값은 `<Response [200]>`임

```python
import requests

indeed_url = "https://kr.indeed.com/jobs?q=python" # 검색할 URL
indeed_result = requests.get(indeed_url) # python으로 검색한 결과

print(indeed_result)
```

3] 검색 결과에서 html 본문 내용 뽑아내기

```python
import requests

indeed_url = "https://kr.indeed.com/jobs?q=python" 
indeed_result = requests.get(indeed_url)

print(indeed_result.text) # 추가된 코드
```

# 전체 코드

```python
import requests

indeed_url = "https://kr.indeed.com/jobs?q=python" 
indeed_result = requests.get(indeed_url)

print(indeed_result.text)
```


# 참고

[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)
[Python Request](https://github.com/psf/requests)
[Pyhotn BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
[import from](http://cloudrain21.com/python-difference-between-import-from-import)