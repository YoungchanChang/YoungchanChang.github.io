---
layout: post
title: 웹스크래핑11. Scrapper Integration
category: python
tags: [python, webscraping]
comments: python
---

# Scrapper Integration

- 파이썬으로 웹 크롤링한 정보와 서버를 합치는 과정

### 과정 상세

- 1.클라이언트에서 요청시 Request에 parameter을 전달한다.

- 2.파이썬에서 웹 크롤링 요청시에 해당 parameter을 이용한다.

- 영향받는 메소드

- 1.get_max_pages()(총 몇 페이지를 반복할 것인지 정보를 가져오는 메소드)

- 2.get_job_list() : **HTML정보**를 가져온 뒤 원하는 **태그 내용**을 지정하는 메소드
    - query값이 달라져도 태그의 모양은 같다.

