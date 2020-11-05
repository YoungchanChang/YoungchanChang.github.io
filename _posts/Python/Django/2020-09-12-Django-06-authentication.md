---
layout: post
title: 파이썬 장고 authentication
category: Django
tags: [python, Django]
comments: Django
---

# 참조

[장고 인증 커스텀](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/)

[유저모델](https://docs.djangoproject.com/en/3.1/ref/contrib/auth/#django.contrib.auth.models.User)

# 인증시스템

- 기존 유저모델이 제공하는 필드 : 

|필드명|타입|옵션|
|------|---|---|
|username        |CharField()   | unique, validators
|first_name      |CharField()   |
|last_name       |CharField()   |
|email           |EmailField()  |
|password        |BooleanField()|
|groups          |BooleanField()|
|user_permissions|BooleanField()|
|is_staff        |BooleanField()|
|is_active       |BooleanField()|
|is_superuser    |BooleanField()|
|last_login      |DateTimeField()|
|date_joined     |DateTimeField()|

### 변경하기

- User Model을 변경하기

- 장고 UserModel이 적절하지 않은 경우가 있다. 예를들어 eamil을 인증시스템으로 사용할 경우가 있다.

- **settings.py에서 설정** 바꾸기

```python
AUTH_USER_MODEL = 'myapp.MyUser'
```

- 만약 프로젝트를 새로 시작한다면, user model을 새로 설치하기를 추천한다. 이 모델은 user model과 동일하게 동작하면서, **향후 필요할 경우에 커스텀** 할 수 있다.

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass
```

- **관리자 페이지에도 등록**해야한다.(admin.py)

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User

admin.site.register(User, UserAdmin)
```