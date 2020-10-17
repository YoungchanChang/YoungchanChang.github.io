---
layout: post
title: 파이썬 장고 Message 
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[메시지 프레임워크](https://docs.djangoproject.com/en/3.1/ref/contrib/messages/)

# 메시지 프레임워크

- 메시지라는 카톡같은 메시지가 아니다. 

- one-time notification이나 flash메시지를 위해서 쓰인다.

- INSTALLED_APPS, middleware이다.

- 문자열을 HTML에서 보여주기

###

- `context 프로세서` 때문에 메시지 변수들을 쓸 수 있다. context 프로세서는 언제 자료를 건네주지?

- messages.error을 하면 태그로 가게 된다.

- 언제 메시지를 쓸 것인지 정해줘야한다.

- view에서 값을 돌려줄 수 있다. meesage.error(reuqest, "Something went wrong")으로 설정할 수 있다.

- 메시지는 refresh하면 없어진다. 오직 한 번만 보여준다.

- `one-time notification`을 보내기

### 중요

- 예외처리에서 사용자에게 **메시지**를 보낼 수도 있따.

- 예외처리에 대한 관점이 조금 바뀌었다.

- 예외처리를 메시지 보내기

- 예외처리와 메시지라....

### 예외 클래스 만들기

- KAKAOEXCEPTION 클래스를 만들 수 있다.

- if else대신에 if raise로 예외처리를 한 다음에 exeception에서 받으면 훨씬 더 깔끔하다!!!

```python
        if error is not None:
            raise KakaoException("Can't get authorization code.")
```

### 스타일링

- absolute div와 inset의 차이는

- `Use .absolute to position an element outside of the normal flow of the document,`

## fixed와 absolute의 차이

- 헤더는 fixed이지만 웰컴은 absolute인 이유는 스크롤했을 때 메시지가 따라올 필요가 없기 때문

[참고](https://zetawiki.com/wiki/CSS_position_absolute,_fixed_%EC%B0%A8%EC%9D%B4_%EC%83%81%EC%84%B8)

### 
