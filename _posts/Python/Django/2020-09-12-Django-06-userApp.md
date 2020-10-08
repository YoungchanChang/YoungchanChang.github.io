---
layout: post
title: 파이썬 장고 UserAPP
category: Django
tags: [python, Django]
comments: Django
---

# 참조

[장고 인증 커스텀](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/)

# Default User교체하기

- 장고의 USERS기능을 확장해야한다. 기존의 USER기능 이외에도 프로필추가 같은 기능이 필요하다.

- 장고에서 user모델을 **덮어쓰기 위한 설정**을 확인한다. **모델은 데이터가 보여지는 모습**이다.



- 1.**User앱 확장**하기

- 2.User애플리케이션 **settings.py에 설치**하기


- 3.유저모델 쓰기 확인. config에 settings에 가서 `AUTH_USER_MODEL = 'users.User'`로 변경한다.

    - ` Dependency on app with no migrations: users`에러가 뜬다. 장고는 users애플리케이션의 model안의 User가 존재한다는 것을 알게 된다.

- 4.Migration하기

    - `python manage.py makemigrations`명령어를 치면 User모델이 생성이 된다. migration파일로 장고가 알아서 만들어준다.

    - `python manage.py migrate`로 실제로 migrate시킨다.

    - 서버를 다시 돌린다.

- 5.admin패널에 USER추가하기

    - admin.py에 user모델 연결하기 admin파일의 역할은 관리자(admin)이 접근(interfacE)가능한 구조를 알려주는 것이다.

- 6.model에 필드 추가하기

    - models.py에 뭘 쓰던 form을 만들어준다. 내가 여기에 쓴 모든 것들을 장고가 form으로 만들어준다.

    - 모델에 넣는 것이면 관리자 창에서 관리할 수 있다.

    - default를 쓰는 이유는 default값이 없다면 **이전에 저장된 값들이 다 null**이 되기 때문이다.

# 추가로 알아두면 좋은 사항

- 장고의 가장 강력한 기능은 관리자 접근을 자동으로 할 수 있는 것이다. metadata를 모델로부터 읽어서 처리할 수 있다.

- 오류 : cannot import name 'AbstactUser' from 'django.contrib.auth.models

- 이유 : 오타이다. AbstractUser라고 적었는지 다시 한 번 확인하자.

- 오류 : django.db.utils.OperationalError: no such table: users_user

- 이유 : db.sqlites3를 삭제한 뒤에 makemigrations를 수행하자.

# 참조


[장고 admin](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)