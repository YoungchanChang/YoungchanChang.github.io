---
layout: post
title: 파이썬 장고 TimeStampedModel
category: Django
tags: [python, Django]
comments: Django
---

# TimeStampedModel

- ROOMS가 만들어질 때나 업데이트 될 때를 알면 좋다. 문제는 이 두 필드가 다른 곳에서도 쓰일 수 있기 때문에 **중복이 될 수 있다는 점**이다.

- **core APP**을 설치해서 중복되는 것을 처리한다.

### TimeStampedModel

- 1.`django-admin startapp core` core는 다른 app에서 재사용가능한 common파일을 만들어준다.

- core에 model을 만들고 이 model을 이용해서 rooms를 확장할 수 있다. User를 제외한 모든 Model은 한 가지 Model으로 부터 확장할 수 있다. 이 Model을 TimeStampedModel이고 이 모델을 확장하면 된다.

- 2.`PROJECT_APPS = ["core.apps.CoreConfig", "users.apps.UsersConfig", "rooms.apps.RoomsConfig"]`을 추가한다.


### TimeStampedModel에서 param 주의사항

- DateField에서 auto_now=true로 하면  **model을 save할 때** date랑 time을 기록할 것이다. auto_now_add는 이 필드는 **Model을 생성**할 때마다 수시로 업데이트 될 것이다. 장고가 새로운 Model을 만들 때마다 날짜와 시간을 넣는다.

- auto_now는 내가 **Model을 저장할 때마다** 새로운 날짜를 적어준다.

```python
from django.db import models

# Create your models here.
class TimeStampedModel(models.Model):

    """ Time STamped Model """

    created = models.DateTimeField(auto_now_add=True)
    updated = models.DateTimeField(auto_now=True)
    class Meta:
        abstract = True
```


### 알아두어야 할 사항

- 파이썬 클래스에 아래와 같은 문구는 데이터베이스에 반영을 안 시키는 부분이다.

```python
    class Meta:
        abstract = True
```




# 참조

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)