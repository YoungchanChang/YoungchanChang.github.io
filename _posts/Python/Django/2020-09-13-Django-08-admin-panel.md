---
layout: post
title: 파이썬 장고 admin Panel기능
category: Django
tags: [python, Django]
comments: Django
---

# Django Admin사이트

- admin.py에서 user를 컨트롤할 클래스라고 명시하는 것이다. 어떤 데이터를 컨트롤할것인지 명시해야한다.

```python
class AuthorAdmin(admin.ModelAdmin):
    pass
admin.site.register(Author, AuthorAdmin)

@admin.register(Author)
class AuthorAdmin(admin.ModelAdmin):
    pass
```


### list_display

- 장고의 admin.py에서 제공하는 것 중에 하나는 list_display이다.

- **list_display로 정의**해주면 자동으로 user를 보여주는 칸을 만들어준다. 

```python
@admin.register(models.User)
class CustomUserAdmin(admin.ModelAdmin):

    list_display = ("username", "gender", "language", "currency", "superhost")

```

### list_filter

- list_filter는 특정 조건에 따른 필터링을 해준다. 그러면 우측에 필터링 칸이 나온다.


```python
@admin.register(models.User)
class CustomUserAdmin(admin.ModelAdmin):

    list_display = ("username", "gender", "language", "currency", "superhost")
    list_filter = ("superhost")
```

# admin panel 기능 확장

- UserAdmin을 임포트한뒤 customUserAdmin에서 상속한다.

- 유저칸에 들어가보면 데이터가 정렬되서 보이게 된다.

- UserAdmin은 User필드를 아직 모른다. Personal Info같은 fieldset을 만든다. 

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from . import models

# Register your models here.
@admin.register(models.User)
class CustomUserAdmin(UserAdmin):

    pass
```

### fieldsets 정의하기

- CustomUserAdmin에서 아래의 필드를 정의하면 자신이 원하는 필드만 나오게 된다.

- 아래 코드에서 UserAdmin의 필드를 확인하려면 객체의 정의부분으로 가면 된다.

```
fieldsets = UserAdmin.fieldsets + (
        ("Custom Profile", {"fields": ("avatar", "gender", "bio", "birthdate", "language", "currency", "superhost")}),)
```

- 장고 인증 시스템과 장고 admin패널, 장고 fieldset, naming, password바꾸기

### 추가 기능들

- custom function도 할 수 있다.

# 참조

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)