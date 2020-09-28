---
layout: post
title: 파이썬 장고 RoomModel
category: Django
tags: [python, Django]
comments: Django
---

# RoomModel

### 나라이름 import하기

- 나라이름에 대한 모델은 Djanggo-countries라이브러리르 쓰면 된다.

- `pipenv install django-countries`

- config/settings.py에서 `THIRD_PARTY_APPS = ['django-countries']`로 등록한다.

- import 팁 `# 파이썬과 관련된 것 # 외부 패키지 # app을 import`순서대로 import하면 보기 좋다.

- room의 소유주는 USER의 정보와 연결해야한다.

### TimeStampedModel에서 param 주의사항

- DateField에서 auto_now=true로 하면  model을 save할 때 date랑 time을 기록할 것이다. auto_now_add는 이 필드는 **Model을 생성**할 때마다 수시로 업데이트 될 것이다. 장고가 새로운 Model을 만들 때마다 날짜와 시간을 넣는다.

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

### Foreign Key

- ROOM에 USER을 추가해도 USER에는 변화가 없다.

- foreingkey는 한 모델을 다른 모델과 연결시켜준다. 연결이 **시작되는 곳은 ROOM**이다.

- USER은 연결되는 정보가 없다!!!

- MANY-TO-ONE

- USER이 1명이고 여러 ROOM을 포함할 수 있다. MANYROOM이 한 USER을 사용하게 된다. 1:다가 된다.

- F.K는 다른 데이터베이스의 ID이다.

- USER테이블의 ID임을 알 수 있다.

- user id임을 알 수 있다.

### MANY TO MANY

- 아빠와 엄마 model은 많은 자식들을 갖을 수 있다. 반면에 "나"의 경우 엄마는 하나밖에 없다. 내가 형제자매를 여럿 갖는 것을 MANY TO MANY라고 한다.

### __str__ 설명

- ROOM에 저장하면 Room object (1)라고 저장된다.

- 장고랑 파이썬은 **클래스를 가지고 string**으로 만들어준다. class들이 가지고 있는 공통의 method는 string method이다

- **파이썬이 class를 발견하면 string처럼 보여준다.** 이 method를 파이썬에서 __str__이라고 표현한다.

- user가 바꿀 수 있다.

- Object를 string으로 보여주면 유용하다!!!

```python
    def __str__(self):
        return self.name
```

- 공통으로 쓸 클래스를 묶는다.

```python
class AbstractItem(core_models.TimeStampedModel):

    """ Abstract Item """

    name = models.CharField(max_length=80)

    class Meta:
        abstract = True

    def __str__(self):
        return self.name


class RoomType(AbstractItem):
    pass

```
 
- `room_type = models.ManyToManyField(RoomType, blank=True)`으로 Many관계를 명시해준다. 그러면 RoomType이 생기게 된다.

- Room Type을 import해준다. 그러면 roomtype을 추가시킬 수 있다.

```python
@admin.register(models.RoomType)
class ItemAdmin(admin):
    pass

```

- AbstractItem클래스를 만들고, 이름필드를 넣어준다. RoomType은 이름이 들어간다. 또한 house rule도 이름이 필요하다. 얘네들은 item이라서 admin패널에서 만들어야한다. amenity도 이름이 필요하다. facilitty도 이름이 필요하다

- AbstractItem인 이유는 카테고리만 다를 뿐 카테고리마다 item이 들어가기 때문이다.

- 여러개나 한 개를 선택할 수 있게 된다. 


### 추가로 알아두어야 할 사항

- import 팁 `# 파이썬과 관련된 것 # 외부 패키지 # app을 import`순서대로 import하면 보기 좋다.

# 참고

- [Date_Time_Field](https://docs.djangoproject.com/en/2.0/ref/models/fields/)