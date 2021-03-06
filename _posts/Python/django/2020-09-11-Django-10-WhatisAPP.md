---
layout: post
title: Django 10 - 파이썬 장고 앱의 개념
category: Django
tags: [python, Django]
comments: Django
---

# App이란

- app은 `특정한 기능을 하는 폴더`이다. 예를 들어서 데이터베이스를 저장하는 기능이 있다.

- 프로젝트는 이런 앱들을 포함하는 집합이다. 앱과 프로젝트는 코드를 정리하는데 도움이 된다.

- `AND`키워드가 들어가면 다른 분류로 들어가야 된다.

### 어플리케이션 생성하기

- 어플리케이션은 하나의 기능을 다루어야 한다. 예를 들어서 room application에 user를 수정, 삭제, 리스트보기, 팔로잉 등의 기능을 추가하면 안 된다. 이렇게 되면 기능이 매우 커지게 된다.

- list앱이 하는 역할은 오직 list생성, 수정, 삭제, 공유하기가 전부이다. list폴더에서는 4가지만 다룬다.

- 장고는 매우 작은 앱으로 이루어져있다. 장고는 언제 어플리케이션을 만들고 만들지 않아야 하는지 알아야 한다.

# 참고

[앱 vs 프로젝트](https://docs.djangoproject.com/en/3.1/intro/tutorial01/)