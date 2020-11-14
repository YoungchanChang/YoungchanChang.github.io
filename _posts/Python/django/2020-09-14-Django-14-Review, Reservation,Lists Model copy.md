---
layout: post
title: 파이썬 장고 ReviewModel, Reservations, Lists
category: Django
tags: [python, Django]
comments: Django
---

# 새로운 모델을 구성

- 새로운 모델(ReviewModel, ReservationModel, Lists Model)을 구성할 때에는 반드시 **환경설정(config)폴더**에서 해당 앱을 설치해야된다.

- 환경설정을 했으면 **모델을 정의**하고 모델을 **관리자 페이지에 등록**하면 된다.

```python
PATH config/setting.py

PROJECT_APPS = [
    "core.apps.CoreConfig",
    "users.apps.UsersConfig",
    "rooms.apps.RoomsConfig",
    "reviews.apps.ReviewsConfig",
]
```

- 2.reviews/models.py에서 데이터 모델 정의하기. F.K를 정의하면 해당 f.k를 통해서 다른 객체의 데이터를 불러올 수 있따.




### 추가로 알아두면 좋은 사항


# 참고

[CASCADE](https://docs.djangoproject.com/en/2.0/ref/models/fields/)

[Meta Option 복수형](https://docs.djangoproject.com/en/2.0/ref/models/options/)

[ordering](https://docs.djangoproject.com/en/2.0/ref/models/options/#ordering)