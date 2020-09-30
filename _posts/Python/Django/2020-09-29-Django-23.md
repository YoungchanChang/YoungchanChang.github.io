---
layout: post
title: 파이썬 장고 seed_amenities command
category: Django
tags: [python, Django]
comments: Django
---

# SEED 만들기

- 장고의 동작원리와 지배하기

- 모델을 바꾸고, admin을 바꾸고.

- 장고 내부에 설명서가 있어서 쉽게 이용할 수 있다.

- 편의시설은 매우 많고 직접 만들기가 불편하다.

- amenities에 씨를 뿌리자.

- Ctrl + Alt + 위 아래를 통해서 멀티 커서를 이용할 수 있다. End누르고 ",누르면 빠르게 이용할 수 있다.

```python
from django.core.management.base import BaseCommand, CommandError
from rooms.models import Amenity
class Command(BaseCommand):
    print("hello")

    help = "This command tells me that he loves me"

    def add_arguments(self, parser):
        parser.add_argument(
            "--times", help="How many time do you wnat me to tell you that i love you?"
        )

    def handle(self, *args, **options):
        amenities = [
            "난방",
            "에어컨",
            "세탁기",
            "건조기",
            "무선 인터넷",
            "아침식사",
            "실내 벽난로",
            "옷걸이",
            "다리미",
            "헤어드라이어",
            "노트북 작업 공간",
            "TV",
            "아기 침대",
            "유아용 식탁의자",
            "셀프 체크인",
            "화재경보기",
            "일산화탄소 경보기",
            "욕실 단독 사용",
            "피아노",
            "해변에 인접",
        ]
        for a in amenities:
            Amenity.objects.create(name=a)
        self.stdout.write(self.style.SUCCESS("Amenities created!!!"))
```

- Amenity는 모듈이고,  mnager가 CRUD를 수행한다.