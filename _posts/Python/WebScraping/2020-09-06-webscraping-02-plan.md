---
layout: post
title: 웹스크래핑02. 웹스크래핑 설계
category: webscraping
tags: [python, webscraping]
comments: python
---

# 과제 주제

- 파이썬을 통해 웹 페이지에서 내가 원하는 정보를 엑셀 파일로 저장

### 과제 진행 순서

- 1.파이썬을 이용해서 웹페이지의 html내용을 가져오기
    - request 모듈을 활용

- 2.가져온 html파일에서 내가 **저장하고자 하는 정보**를 추출
    - beautifulsoup를 활용
    - html태그 구조를 활용

- 3.**웹 페이지의 규칙성**을 활용해서 여러 페이지에서 내용 추출하기
    - RESTFUL API방식을 활용한다.

- 4.CSV로 저장하기
    - PANDAS활용



# 참고

[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)

[Python Request](https://github.com/psf/requests)

[Pyhotn BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

[import from](http://cloudrain21.com/python-difference-between-import-from-import)