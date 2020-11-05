---
layout: post
title: 파이썬 장고 raw_ids and Inline Admin
category: Django
tags: [python, Django]
comments: Django
---

### raw_ids

- 유저들이 많아지면 리스트가 매우 커진다. id로 접근하고 싶을 때 쓴다.

- `raw_id_fields = ("host",)`

- 긴 리스트 대신에 user admin을 쓸 수 있다. amenities를 쓸 수도 있다.

### inline model

- admin안에 또 다른 admin을 넣는다.

- photo는 room에 소속되어있다. 그래서 **room에서 해당 photo를 관리**하는 것이 편하다.

- admin에 새로운 모델을 만든 뒤에, **Inline클래스를 상속받는다. 해당 모델에 객체를 선언한다.**

- room에는 사진 셋트들이 들어있다. photos에 가서 photo를 추가하고 저장하는 것 보다, admin의  photo에 추가하는게 낫다.

- 장고가 자동으로 room의 foreing key를 가지고 있는 이미지를 집어넣는다.

- 장고는 똑똑해서 foreing key가 room들과 연결된 것을 알 수 있다.

- TabularInline도 있지만 StackedInline도 있다. 모양이 약간 다르다.

- F.K를 쓰면 Django는 model과 room의 관계를 알아차릴 수 있고, 모든 것을 알아서 다 해준다.

###  User에서 Room 관리해보기

```python
from rooms import models as md
# Register your models here.

class PhotoInline(admin.TabularInline):

    model = md.Room

@admin.register(models.User)
class CustomUserAdmin(UserAdmin):
    """ Custom User Admin """

    inlines = (PhotoInline,)
```

# model이 저장될 때 가로채기

- 상속받은 Model의 기능을 override하기.

- seoul을 입력했을 때 Seoul로 변화시켜주기.(대문자 -> 소문자로 변환)

- 예제코드를 보면, save메소드를 override하면서 do_something()을 한다.

```python
from django.db import models

class Blog(models.Model):
    name = models.CharField(max_length=100)
    tagline = models.TextField()

    def save(self, *args, **kwargs):
        do_something()
        super().save(*args, **kwargs)  # Call the "real" save() method.
        do_something_else()
```

- django.admin도 save_model을 가지고 있다. 사용 용도가 다르다.


# 참고

[raw-id-field](https://docs.djangoproject.com/en/2.2/ref/contrib/admin/#django.contrib.admin.InlineModelAdmin.raw_id_fields)

[inline Model Admin](https://docs.djangoproject.com/en/2.2/ref/contrib/admin/#django.contrib.admin.InlineModelAdmin)

[overriding](https://docs.djangoproject.com/en/2.2/topics/db/models/#overriding-predefined-model-methods)