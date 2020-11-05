---
layout: post
title: 파이썬 장고 seed
category: Django
tags: [python, Django]
comments: Django
---


# 참고

[장고시드](https://pypi.org/project/django-seed/)

# SEED 만들기

- Django Seed는 faker라이브러리를 사용한다.

- 나의 모듈을 보고 장고시드는 내가 갖고 있는 field를 본다. Integer이라면 integer, time이라면 time을 넣는다.


- 장고시드에 random값을 부여하기 위해서는 model과 몇 개를 만들것인지를 건네주면 된다. seeder내부의 faker라이브러리가 columntype에 적절한 값들을 랜덤으로 부여해준다.

- column name에 따라서 custom functio을 지정할 수 있다. 람다식으로 지정할 수 있다.

- 장고 시드 설치하기

- 장고 시드는 faciliteis나 amenities같은 foreinkey를 쓸 때 안 좋다.

- default값을 넣고, type값을 넣어야 한다. 안 넣으면 오류 발생

- `python manage.py seed_user --number=1`명령어를 전달하면 type이 string으로 처리되어서 에러가 된다. 따라서 type을 정해줘야한다.

- `default=2`사용자가 값을 잘못 넣었을 경우를 대비해서 해당 코드를 넣어야 한다.

```python
from django.core.management.base import BaseCommand, CommandError
from django_seed import Seed
from users.models import User


class Command(BaseCommand):
    print("hello")

    help = "This command create many users"

    def add_arguments(self, parser):
        parser.add_argument(
            "--number",
            default=1,
            type=int,
            help="How many users do you want me to create you that i love you?",
        )

    def handle(self, *args, **options):
        number = options.get("number", 1)
        seeder = Seed.seeder()
        seeder.add_entity(User, number, {"is_staff": False, "is_superuser": False})
        seeder.execute()
        self.stdout.write(self.style.SUCCESS(f"{number} created!!!"))
```

### 한국인 유저 생성하기

- seeder에 (locale='ko_KR')는 작동하지 않는다. 반면 seeder의 모객체인 Faker('ko_KR')는 작동한다. 따라서 해당 객체를 이용하면 한국인 유저를 생성할 수 있다.

- 실험해보니 한국이름과 한국 주소만 생성이 가능하다. sentence()나 text()는 안 된다.

```python
        seeder = Seed.seeder(locale='ko_KR')
        faker = Faker('ko_KR')

        seeder.add_entity(User, number, {
            "first_name": lambda x: faker.name()[0:1],
            "last_name": lambda x: faker.name()[1:4],
            "is_staff": False,
            "is_superuser": False
        })
```