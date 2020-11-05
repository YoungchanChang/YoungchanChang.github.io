---
layout: post
title: 파이썬 장고 admin Panel기능
category: Django
tags: [python, Django]
comments: Django
---

# 참조

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)

[admin.py기능 확장](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/)

# Django Admin사이트

- admin.py에서 user를 컨트롤할 클래스라고 명시하는 것이다. 어떤 데이터를 컨트롤할것인지 명시해야한다. 사이트 명시 방법에는 2가지가 있다. 아래 참조

```python
class AuthorAdmin(admin.ModelAdmin):
    pass
admin.site.register(Author, AuthorAdmin)

@admin.register(Author)
class AuthorAdmin(admin.ModelAdmin):
    pass
```

### list_display

- **list_display로 정의**해주면 자동으로 user를 보여주는 칸을 만들어준다. list_display는 어떤 필드가 관리자 페이지에서 보여질지 정의해준다.

### list_filter

- list_filter는 특정 조건에 따른 필터링을 해준다. 그러면 **우측에 필터링 칸**이 나온다.

# admin panel 기능 확장

- UserAdmin을 임포트한뒤 customUserAdmin에서 상속한다.

- 달라진점 : **useradmin 필터가 달라져있다. 파란색창으로 묶여있다. 패스워드 바꾸는 기능**도 생겼다.

- UserAdmin에 **내가 쓰는 필드들을 알려줘야**한다. 이 때 사용하는 것이 fieldset이다.

### fieldsets 정의하기

- 필드셋은 admin에서 추가하거나 바꾸는 페이지에서 사용된다.

- CustomUserAdmin에서 아래의 필드를 정의하면 자신이 원하는 필드만 나오게 된다.


### 추가 기능들

- custom function도 할 수 있다.
