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

### 추상 클래스 만들기

- 3.core/models.py정의

- abstractModel은 **데이터베이스에는 나타나지 않는 모델**이다. 대다수의 abstractModel은 확장을 목적으로 한다. users폴더에서 models.py로 들어가서 보면 AbastractUser을 쓰고 있다. 코드에서만 상속을 받는다.


### 사용하는 쪽에서 import하기

- 4.해당 모델을 쓰는 쪽에서 import한다. 이 모델은 많은 곳에서 쓰인다.
 

### 알아두어야 할 사항

- 파이썬 클래스에 아래와 같은 문구는 데이터베이스에 반영을 안 시키는 부분이다.

```python
    class Meta:
        abstract = True
```


# 장고의 특징

- config/settings.py에서 `PROJECT_APPS = ["users.apps.UsersConfig", "rooms.apps.RoosConfig"]`코드 추가

- rooms/models.py에서 ORM정의하기

```python
from django.db import models
class Room(models.Model):

    """ Room Model Definitino """

    pass
```

- rooms/admin.py에서 room의 모델 쓰겠다고 선언. 화면 새로고침하면 administration에 ROOMS를 볼 수 있다.

# 참조

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)