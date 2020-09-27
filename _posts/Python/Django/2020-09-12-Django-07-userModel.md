---
layout: post
title: 파이썬 장고 UserModel
category: Django
tags: [python, Django]
comments: Django
---

# Django의 사용자 데이터 모델링하기

- 데이터필드 추가시 주의할 점: 디폴트를 줘야함 안 주면 이전 rows들이 null값이 됨. null값을 설정으로 허용해주면 된다.

- 반드시!!! makemigrations다음에 `python manage.py migrate`로 실제로 migrate시켜야 모델에 반영이 된다.

```python
class User(AbstractUser):

    # 변수를 선언하고 해당 변수를 튜플안에 넣는다. 그리고 데이터베이스 모델링시에 choice에 넣는다.

    GENDER_MALE = "male"
    GENDER_FEMALE = "female"
    GENDER_OTHER = "other"

    GENDER_CHOICES = (
        (GENDER_MALE, "Male"),
        (GENDER_FEMALE, "Female"),
        (GENDER_OTHER, "Other"),
    )

    LANGUAGE_ENGLISH = "eng"
    LANGUAGE_KOREAN = "kr"

    LANGUAGE_CHOICES = ((LANGUAGE_ENGLISH, "English"), (LANGUAGE_KOREAN, "Korean"))

    CURRENCY_USD = "usd"
    CURRENCY_KRW = "krw"

    CURRENCY_CHOICES = ((CURRENCY_USD, "USD"), (CURRENCY_USD, "KRW"))

    # 여기서 ImageField()는 `pipenv install Pillow`로 설치해야한다.
    avatar = models.ImageField(null=True)
    gender = models.CharField(choices=GENDER_CHOICES, max_length=10, null=True)

    # null은 database를 위한 것이고, 실제로 제출했을 시 입력값을 넣지 않는다고 나온다. `blank=True`로 설정해야지 from에 유지된다.
    bio = models.TextField(default="", blank=True)
    birthdate = models.DateField(null=True)
    language = models.CharField(
        choices=LANGUAGE_CHOICES, max_length=2, null=True, blank=True
    )

    currency = models.CharField(
        choices=CURRENCY_CHOICES, max_length=3, null=True, blank=True
    )


    # superhost로 인증받은 사용자를 의미한다.
    superhost = models.BooleanField(default=False)
```

- 사용자에게 입력받을 정보를 데이터 모델링을 한 것이다.

- 장고의 좋은점은 데이터를 모델링하면 **알아서 admin패널**을 만들어준 점이다!!!!!!!!!

- admin은 프로그래머용이다.


# 참조
[장고 인증 커스텀](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/) AUTH USER

[장고 choices](https://docs.djangoproject.com/en/2.0/ref/models/fields/)

[장고 admin site](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/)