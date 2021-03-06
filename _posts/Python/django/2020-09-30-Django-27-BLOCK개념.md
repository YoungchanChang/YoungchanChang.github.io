---
layout: post
title: 파이썬 장고 HomeView Intro
category: Django
tags: [python, Django]
comments: Django
---

# HTTP 기본 동작

- 뷰는 내가 해당 URL로 매번 들어갈 때마다 HTTP Request를 생성한다.

- HTTP Response를 해줘야한다. Request - Response

- Request는 유저가 로그인했는지 안했는지 알 수 있다. 로그인과 비밀번호가 입력되었는지 알 수 있다.

- 장고는 Request를 Python Object로 만들어서 모든 view에 대해서 넘겨준다.

- `Request`가 오면 해당 Request를 분석한 뒤에 요청 데이터를 `Template`에 넘겨서 `Render`를 수행한 뒤 결과값을 return한다. 읽을 수 있도록 `context`에 넘겨준다.

- `from django.shortcuts import render`는 HttpResponse 안에 html을 넣어서 보내줄 수가 있다.

### Rendering

- Render은 만들다는 뜻이다. 요리를 만들 때, 재료를 갖고와서 만드는 행위를 하듯, 어떤 변수값을 템플릿에다가 넣어주면 눈에 보이게 만들어주는 것이 Render이다.

- 템플릿을 통해 **Logic을** 짤 수 있다.

- context의 이름은 변수명과 같을 필요는 없다. template에서는 변수명이 같아야 한다.!!! potato면 html에서도 potato여야한다.

- view이름은 urls.py의 이름과 같아야 한다.

# DB로부터 데이터베이스에 가져와서 object를 가져오기

- 

# Extending Templates

- 구조가 똑같으면 중복을 제거하는 편이 좋다. **템플릿이 템플릿을 상속**해서 쓸 수 있다.

- base를 render하지 않더라도, 모든 템플릿은 base를 쓰게 된다. Model을 쓰지는 않지만 다른 Model이 쓰는 것처럼 부모 템플릿을 만들 수 있다.

- **부모 템플릿**

- Extending하기 위해서는 선언하면 된다. 단순하게 `rooms/home.html`로 확장하면 된다.

### Block의 개념

- Block은 하나의 창과 같은 것이다. 자식 템플릿이 부모 템플릿에게 넘겨주는 창이다.

- 부모 템플릿과 자식 템플릿의 **연결고리**

- Block은 자식 템플릿이 넣을 수 있는 것이다.

- **base.html다음에 block**을 쓴다. base에서 extend했기 때문에 쓸 수 있다.

- block을 쓸 수 잇는 이유는 extends했기 때문이다.

- extend하고 블럭을 사용했기 때문에 쓸 수 있다. base.html에서 블락으로 선언한 부분을 이용할 수 있다.

- **base로부터 extending한다!!!**

- 기억해야 할 것 : block은 창문이다. 자식이 부모 템플릿에게 content를 집어넣을 수 있는

- 파일들을 작게 쪼개면 좋다. Divide and conquere!!!

# 문제점

- `<a href="/">Nbnb</a>` 이런 식으로 코드를 구성하면 사용하는 템플릿마다 해당 url이 다르기 때문에 문제가 생길 수 있다.

# 참고

[장고시드](https://pypi.org/project/django-seed/)

[페이커 깃허브](https://github.com/joke2k/faker/)

[페이커 공식 라이브러리](https://faker.readthedocs.io/en/master/)