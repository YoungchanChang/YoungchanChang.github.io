---
layout: post
title: 파이썬 장고 RoomModel
category: Django
tags: [python, Django]
comments: Django
---

# RoomModel 사용하겠다고 선언하기

# 장고에서 admin사용하기

- config/settings.py에서 `PROJECT_APPS = ["users.apps.UsersConfig", "rooms.apps.RoosConfig"]` 해당 앱을 쓰겠다는 코드 추가

- rooms/admin.py에서 room의 모델 쓰겠다고 선언. 화면 새로고침하면 administration에 ROOMS를 볼 수 있다.



### 관리자 페이지에서 처리

- 관리자 페이지에서 해당 RoomType을 쓸 수 있게 등록해준다.

```python
@admin.register(models.RoomType)
class ItemAdmin(admin):
    pass

```



# 추가로 알아두면 좋은 사항

### 복수형으로 만들기

- 복수형으로 만들기 위해서는 메타데이터를 추가한다.

```python
    class Meta:
        verbose_name = "House Rule"
```

### 순서 정렬하기

- 정렬하고 싶은 옵션을 적어준다. 첫번째 정렬하고, 두번째 정렬하고 싶은 순서대로 적어주면 된다.

- `ordering = ("name", "price", "bedrooms")`


# 참고

[CASCADE](https://docs.djangoproject.com/en/2.0/ref/models/fields/)

[Meta Option 복수형](https://docs.djangoproject.com/en/2.0/ref/models/options/)

[ordering](https://docs.djangoproject.com/en/2.0/ref/models/options/#ordering)