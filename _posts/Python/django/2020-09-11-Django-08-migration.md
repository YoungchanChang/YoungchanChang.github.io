---
layout: post
title: Django 08 - migratation
category: Django
tags: [python, Django]
comments: Django
---

> [Migration](https://wayhome25.github.io/django/2017/03/20/django-ep6-migrations/)

# migratation

- 모델(데이터베이스의 구조) 변경내역 히스토리 관리

- 모델 변경내역을 DB sCHEMA로 반영시키는 방법을 제공

### Django에서 migration 파일 생성, 적용하기

- `python manage.py makemigrations` 장고는 데이터 모델(데이터)를 확인하고 migratation파일을 만든다. 만들어진 파일은 migrations폴더에 있다.

- `python manage.py migrate`명령어를 수행하면 해당 마이그레이션을 `실제 DB에 반영`한다.

- 장고 코드를 사용해서 users, admin, auth, sessions 그 밖의 다양한 것들을 저장할 수 있다. "http://127.0.0.1:8000/admin"로 가게 되면 에러가 뜬다. 장고와 데이터베이스가 연동되지 않았다고 뜬다. SQL데이터베이스는 엑셀과 같이 생겼다. 행과 열이 있다. 

### 참고로 알아둬야 할 사항

- 장고에는 migration system이 있다. DB의 경우, 하나의 상태에서 다른 데이터 유형으로 바꿔주는 기능이다. **데이터의 유형이 바뀔 때마다 migrate이 필요**하다.

- migrate : one db -> another db. 하나의 구조를 다른 DB로 이주시킨다.

- 뒤에 UserAPP을 변경할 때, db.sqlite3를 삭제해야 하는 경우가 있다.
