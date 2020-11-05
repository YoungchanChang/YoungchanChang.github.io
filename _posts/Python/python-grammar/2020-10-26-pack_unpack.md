---
layout: post
title: kwargs
category: python
tags: [python, dictionary]
comments: true
---

# 파이썬 버전 바꾸기

- pack, unpack 쪼개지 않으면 **tuple이 되서** 돌아온다!!!!!!!!!!!!!!!!!!

```python
    the_list, _ = models.List.objects.get_or_create(
        user=request.user, name="My Favourites Houses"
    )
    the_list.rooms.add(room)
```

- 