---
layout: post
title: 파이썬 장고 RoomModel RDBM
category: Django
tags: [python, Django]
comments: Django
---


# RDBM에서 관계 맺기

### Foreign Key

- ROOM에서 USER의 정보가 필요하다면 **ForeignKey로** 해당 테이블을 불러올 수 있다.

- foreingkey는 한 모델을 다른 모델과 연결시켜준다. 연결이 **시작되는 곳은 선언한 ROOM**이다.

- 한명의 유저가 여러개의 룸을 선택할 수 있다. 유저는 한명 : 방은 여러개 구조가 된다.

- F.K는 **다른 테이블의 ID**를 쓸 수 있다. Room의 F.K는 USER테이블의 ID이다.


### MANY-TO-MANY

- 아빠와 엄마 model은 많은 자식들을 갖을 수 있다. 반면에 "나"의 경우 엄마는 하나밖에 없다. 내가 형제자매를 여럿 갖는 것을 MANY TO MANY라고 한다.

### 옵션 on_delete

- `host = models.ForeignKey(user_models.User, on_delete=models.CASCADE)`에서 on_delete의 의미

- host가 삭제됬을 때 room을 어떻게 처리할지를 정해주는 것이다. on_delete는 room으로 무엇을 할 것인지 정해주느 ㄴ것이다.

- cascade는 폭포의 의미로 하나의 행동이 모든 것에 영향을 주는 것을 의미한다. user가 삭제되면 room도 삭제된다.



# 추상 클래스 만들기

- rooms/models.py에서 모델 정의하기

```python
from django.db import models
class Room(models.Model):

    """ Room Model Definitino """

    pass
```

### 공통으로 쓸 클래스를 묶는다.

- TimeStampedModel과 같이 공통으로 쓰는 모델을 추상클래스로 만들고 상속받게 할 수 있다.

- abstractModel은 **데이터베이스에는 나타나지 않는 모델**이다. 대다수의 abstractModel은 확장을 목적으로 한다. users폴더에서 models.py로 들어가서 보면 AbastractUser을 쓰고 있다. 코드에서만 상속을 받는다.

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
- AbstractItem클래스를 만들고, 이름필드를 넣어준다. RoomType은 이름이 들어간다. 또한 house rule도 이름이 필요하다. 얘네들은 item이라서 admin패널에서 만들어야한다. amenity도 이름이 필요하다. facilitty도 이름이 필요하다

- AbstractItem인 이유는 카테고리만 다를 뿐 카테고리마다 item이 들어가기 때문이다.

- 여러개나 한 개를 선택할 수 있게 된다. 

### RoomType을 만드는 이유

- RoomType객체를 만드는 이유는 **admin패널**에서 **관리**하기 위해서이다!!!

- **admin패널에 넣어야 할지 프로그래머가 관리할지**는 사용자 선택이다.

```python
class RoomType(AbstractItem):
    """ RoomType Object Definition """
    pass

```

- RoomType의 모델을 생성했으면 admin에 등록해서 추가하게 만든다.



# 추가로 알아두면 좋은 사항

### __str__ 설명

- 장고는 **관리자 페이지에서 객체를 보여줄 때** 해당 메소드를 쓴다. 그러므로 언제나 str()메소드를 사람이 읽을 수 있게 반환하는 것이 좋다.

- 장고랑 파이썬은 **클래스를 가지고 string**으로 만들어준다. class들이 가지고 있는 공통의 method는 string method이다

- **파이썬이 class를 발견하면 string처럼 보여준다.** 이 method를 파이썬에서 __str__이라고 표현한다.

- Object를 string으로 보여주면 유용하다!!!

```python
    def __str__(self):
        return self.name
```

### Third_PARTY 사용하는 방법

- 나라이름에 대한 모델은 Djanggo-countries라이브러리를 쓰면 된다.

- `pipenv install django-countries`

- config/settings.py에서 `THIRD_PARTY_APPS = ['django-countries']`로 등록한다.

- import 팁 `# 파이썬과 관련된 것 # 외부 패키지 # app을 import`순서대로 import하면 보기 좋다.

- room의 소유주는 USER의 정보와 연결해야한다.



### 추가로 알아두어야 할 사항

- import 팁 `# 파이썬과 관련된 것 # 외부 패키지 # app을 import`순서대로 import하면 보기 좋다.

# 참고

- [__str__](https://docs.djangoproject.com/en/3.1/ref/models/instances/)

- [Date_Time_Field](https://docs.djangoproject.com/en/2.0/ref/models/fields/)