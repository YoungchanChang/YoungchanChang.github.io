---
layout: post
title: 파이썬 장고 Managers and QuerySets
category: Django
tags: [python, Django]
comments: Django
---

# Managers and QuerySets

### Manager

- 장고에서 데이터베이스로부터 elements를 가져올 수 있게 하는 객체인 Manager가 있다. Manager의 역할은 파이썬을 이용해서, sql을 쓰지 않고 DB로부터 데이터를 가져올 수 있게 해준다.

### 콘솔을 사용해서 장고로 들어가기

- 파이썬 콘솔 안에서 데이터 가져오기

- 단순히 pyhton명령어를 치면 콘솔로 들어가지지 않는다. `python manage.py shell` 명령어를 쳐야 한다.

```console
python manage.py shell
>>> from users.models import User
>>> User
<class 'users.models.User'>
>>> User.objects
<django.contrib.auth.models.UserManager object at 0x03B1FC10>
>>> User.objects.all()
<QuerySet [<User: msi>, <User: test>]>
all_user = User.objects.all()
all_user.filter(superhost=True)
>>> msi = User.objects.get(username="msi")
>>> print(msi)

>>> vars(msi)
>>> dir(msi)
```


### 2가지 중요한 메소드

- 유저객체는 AbstractUser로부터 상속받았다. AbsctractUser안에 `objects = UserManager()`라는 선언이 들어가있다. **UserManager은 DB와 사이트를 이어**준다.

- 클래스 내부의 속성들 (필드, 메소드)를 확인하기 위해서 vars()와 dir()을 쓴다. 이 둘의 차이점은 dir()은 부모의 부모 객체까지 파고들어서 정보를 보여준다는 점이다.

- 매니저를 이용해서 `User.objects.all()`명령어를 수행하면 모든 QuerySet을 가져올 수 있게 해준다. QuerySet은 db안의 모든 객체의 정보를 포함하게 해준다. 실제 반환 결과는 오른쪽과 같다.`<QuerySet [<User: msi>, <User: test>]>`

- obejcts(Manager)에서 filter()메소드는 QuerySet을 반환하는 반면, User.object()메소드는 객체를 **바로 반환**해준다.


### 다른 객체에 접근하기

- 바로 반환된 객체에서는 많은 기능을 제공하고 있다. 해당하는 기능은 vars()나 dir()로 확인할 수 있다. dir(msi)를 해보면 끝이 set으로 끝나는 필드들이 존재한다. `list_set, room_set, review_set`등이 있다. 내가 다른 객체를 지정하지 않더라도, 다른 객체가 나를 지정한 곳에 접근해줄 수 있는 키워드가 `set`이다.

- 다른 객체에서 F.K나 P.K를 썻다면, 나의 객체에 `해당객체_set`으로 보이게 된다. 해당 set을 통해서 다른 객체에 접근할 수 있다.

- 아래 예시는 해당 set을 이용해서 rooms에도 접근할 수 있다.

```console
>>> msi.room_set
<django.db.models.fields.related_descriptors.create_reverse_many_to_one_manager.<locals>.RelatedManager object at 0x03BFD550
>>> msi.room_set.all()
<QuerySet [<Room: T>]>
```

- `?_set`은 **elements**가 foreign keys에 접근할 수 잇는 방법이다.


### vars()와 dirs()의 차이

- 파이썬 x.__dict__와 dir(x)처럼 딕셔너리를 반환한다. 모든 클래스의 속성들을 반홚낟.

- 파이썬에서는 메소드도 속성이다. python은 m.__dict__에서 메소드를 찾는다.  없으면 상위 객체에서 찾는다.

- vars()보다 dir()이 더 많은 메소드를 반환한다. Base까지 반환한다.

# 참고

[Making quries](https://docs.djangoproject.com/en/2.2/topics/db/queries/)

[var과 dir차이](https://stackoverflow.com/questions/980249/difference-between-dir-and-vars-keys-in-python)

[QuerySet](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#django.db.models.query.QuerySet)