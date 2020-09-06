---
layout: post
title: 웹스크래핑06. REST API방식을 활용하여 여러 페이지 내용 추출하기
category: python
tags: [python, webscraping]
comments: python
---

### 웹 페이지의 규칙성을 활용해서 여러 페이지에서 내용 추출하기

    - HTTP 요청 메서드 중 GET방식을 사용한다.
    
### 과제 진행 순서

1] find()메소드로 pagination 부분에 해당하는 태그 내용만 추출.

2) find_all()메소드로 **a태그의 내용만 추출**. 리스트값 반환

3] for in 구문을 활용하여 리스트 중에서 번호에 해당하는 부분만 추출. 마지막은 next부분으로 숫자가 아님으로 출력하지 않는다.

4] 요청 파라미터 만들기



# 참고

[RESTFUL API](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)
[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)
[import from](http://cloudrain21.com/python-difference-between-import-from-import)