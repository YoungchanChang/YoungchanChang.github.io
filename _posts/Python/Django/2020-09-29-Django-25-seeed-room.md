---
layout: post
title: 파이썬 장고 seed Room
category: Django
tags: [python, Django]
comments: Django
---

# Seed Room

- User와 똑같이 만드려고 하면, `django_seed.exceptions.SeederException: Field rooms.Room.host cannot be null`에러가 뜬다.

- **seeder가 foreing key를 만들지 못하기 때문**이다. DB에서 유저데이터를 가져와서 매칭시켜줘야 한다.

- `all_users = user_models.User.objects.all()`로 모든 유저를 가져올 수 있지만, 좋은 방법은 아니다. 특정 유저의 수만 보여주는 것이 중요하다.(Pagination!!!!)

### F.K처리하는 방법

- seeder에서 해당 function은 선택 필드를 주면 된다.

- 장고에 faker 라이브러리르 쓸 수 있다.

# Photo 만들기 - MANY TO MANY 처리하는 방법!!!!!

- 방을 만들고 방의 ID를 photo에다가 전달해야된다. seeder의 seeder.execute()는 방의 ID를 반환한다. 이 형태는 dictionary로써, key:value()의 값을 갖는다.

- create.value()로 value()값만을 가져온다.

- photo의 랜덤 숫자를 만들고, room으로 할당한다. photos의 랜던 번호를 뽑기 위해서 3에서 15로 한다.

- 생성된 모든 room을 p.k로 그 room을 갖고, 루프를 돌면서 3부터 17까지 사진을 만든다.

- file을 준다.

# Amenitis 추가하기

- `list_model.rooms.add(*to_add)`는 array안에 있는 요소를 선택할 때 쓰인다.

# 참고

[장고시드](https://pypi.org/project/django-seed/)

[페이커 깃허브](https://github.com/joke2k/faker/)

[페이커 공식 라이브러리](https://faker.readthedocs.io/en/master/)