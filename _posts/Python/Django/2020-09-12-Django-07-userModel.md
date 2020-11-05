---
layout: post
title: 파이썬 장고 UserModel
category: Django
tags: [python, Django]
comments: Django
---

# Django의 사용자 데이터 모델링하기

- 데이터필드 추가시 주의할 점: 디폴트를 줘야함 안 주면 이전 rows들이 null값이 됨. null값을 설정으로 허용해주면 된다.

- 반드시!!! makemigrations다음에 `python manage.py migrate`로 실제로 migrate시켜야 모델에 반영이 된다.

- 사용자에게 입력받을 정보를 데이터 모델링을 한 것이다.

- 장고의 좋은점은 데이터를 모델링하면 **알아서 admin패널**을 만들어준 점이다!!!!!!!!!

- admin은 프로그래머용이다.


# 참조
[장고 인증 커스텀](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/) AUTH USER

[장고 choices](https://docs.djangoproject.com/en/2.0/ref/models/fields/)

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)