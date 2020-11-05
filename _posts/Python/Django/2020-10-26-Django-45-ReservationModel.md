---
layout: post
title: ModelManager만들기
category: Django
tags: [python, Django]
comments: Django
---

# ModelManager

- 사용자가 DB를 더 잘 다루기 위해서 아래와 같이 수행해야된다.

- 1.Manager를 받는다. manager은 models.py를 상속받는다. CustomReservationManager(model.Manager)

- 2.models.py에서 objects=managers.CustomResrvationManager()로 정의한다.

- 3.manager에서 메소드를 정의한다.

- 4.해당 model을 쓸 수 있다.

# 정보가 없을 때 404페이지 뜨게 하기

- GET으로 특정 정보를 가져오려고 할 때, 존재하지 않는다면 404페이지를 띄워야 한다.

- 사용자가 쓰지 않는 페이지는 에러인 Http404()를 발생시킬 수 있다.

- get_or_none()으로 새로운 타입을 만들 수 있다.

