---
layout: post
title: 파이썬 장고 RoomModel
category: Django
tags: [python, Django]
comments: Django
---


# Photo

- 방은 사용자에게 소속되듯이, 사진은 방에 소속된다. 따라서 photo를 room의 F.K로 만들면 된다.

- Room에는 사진의 정보가 없고, 사진에서 f.k로 room과 관계를 맺는다.

- 최종 관계를 보면 photo->room->user이다. 사진에서 room정보를 갖고 있고, room은 user정보를 갖고 있다.


### RoomModel

- ForeignKey를 String을 이용해서 만들 수 있다.

# 참고

[CASCADE](https://docs.djangoproject.com/en/2.0/ref/models/fields/)

[Meta Option 복수형](https://docs.djangoproject.com/en/2.0/ref/models/options/)

[ordering](https://docs.djangoproject.com/en/2.0/ref/models/options/#ordering)