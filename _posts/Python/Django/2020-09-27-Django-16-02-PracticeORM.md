---
layout: post
title: 파이썬 장고 Practicing Django ORM
category: Django
tags: [python, Django]
comments: Django
---

### Practicing Django ORM

- `객체.연관객체_set.all()`로 만들면 해당객체의 정보를 얻어낼 수 있다.

```console
>>> msi.review_set.all() 
<QuerySet [<Review: I love this house - T>]>
```

- set은 `foreing key의 대상이 element를 얻어내는 방법이다.`

### set의 활용용도

- set을 통하면 **사용자와 관련된 모든 정보들을 가져올 수 있다!!!**

- Airbnb라면 사용자에 의해 생성된 모든 room들을 가져올 수 있게끔 해야한다. 인스타그램을 갖고 있으면 인스타그램 프로피롤 가서 업로드된 사진들을 전부 ㄱ자ㅕ와얗나다.

- related_name은 user가 우리를 어떻게 찾는지 명시해주는 것이다.

### room_set 별명지어주기

- F.K속성으로 "related_name"을 주면 해당 객체에게 내가 어떻게 불려질 수 있는지 **별명을 정해줄** 수 있다.

- 그러면 기존에 **room_set대신에 rooms로 접근**할 수 있다.

```python
    host = models.ForeignKey("users.User", related_name="rooms", on_delete=models.CASCADE)
```

```console
>>> from users.models import User
>>> msi = User.objects.get(username="msi")
>>> msi.room_set (이전에는 됬지만 related_name 설정하고 안 됨
>>> msi.rooms
```

- 하나의 object가 foreing keys에 접근할 수 있다.

- 장고에서는 `pk와 id가 동의어`이다.

- **review에서 room을 가리키고 있었다면**, room은 reivew_set을 갖을 수 있다.

```console
>>> from rooms.models import Room
>>> room = Room.objects.get(id=1)
>>> room = Room.objects.get(pk=1)
>>> room.review_set
<django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager object at 0x009757D0>
```

### 공식문서 참조해보기

- set과 set을 이용해 데이터를 가져오는 방법을 배웠다.

- 공식문서에서 나온 예제

```python
>>> b = Blog.objects.get(id=1)
>>> b.entries.all() # Returns all Entry objects related to Blog.

# b.entries is a Manager that returns QuerySets.
>>> b.entries.filter(headline__contains='Lennon')
>>> b.entries.count()
```

- filter를 이용하는 방법

```
>>> startswith = User.objects.filter(username_startswith="msi")
>>> print(startswith)
```

- **related_name**은 대상이 나를 찾는 방식을 지정하는 것이다.


### Amenity에서 rooms사용하기

- 특정 Amenity를 사용하는 모든 room들 가져오기

- **related_name을 사용하는 이유는 target을 위한 것**이다!!! target에서 접근하기 쉽게 사용하는 것이다.

```console
>>> from rooms.models import Amenity
>>> Amenity.objects.room_set
>>> Amenity.objects.all()
>>> a= Amenity.objects.get(id=1)
>>> a.room_set
>>> a.room_set.all()
```

### ItemAdmin설정

- ItemAdmin에서도 설정을 해준다. 그러면 여러 admin에서 설정이 되있게 된다.

```python
@admin.register(models.RoomType, models.Amenity, models.Facility, models.HouseRule)
class ItemAdmin(admin.ModelAdmin):

    """ Item Admin Definition """

    list_display = ("name", "used_by")

    def used_by(self, obj):
        return obj.rooms.count()

    pass

```

### vars()와 dirs()의 차이

- 파이썬 x.__dict__와 dir(x)처럼 딕셔너리를 반환한다. 모든 클래스의 속성들을 반홚낟.

- 파이썬에서는 메소드도 속성이다. python은 m.__dict__에서 메소드를 찾는다.  없으면 상위 객체에서 찾는다.

- vars()보다 dir()이 더 많은 메소드를 반환한다. Base까지 반환한다.

# 참고

[Making quries](https://docs.djangoproject.com/en/2.2/topics/db/queries/)

[var과 dir차이](https://stackoverflow.com/questions/980249/difference-between-dir-and-vars-keys-in-python)

[QuerySet](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#django.db.models.query.QuerySet)