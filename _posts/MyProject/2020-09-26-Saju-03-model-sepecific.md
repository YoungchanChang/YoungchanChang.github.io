---
layout: post
title: 모델 기본 틀 만들기
category: MyProject
tags: [MyProject]
comments: MyProject
---


# DB 구성

- 생년월일시에 모르겠음도 있어야 한다. 그리고 생년월일시는 원본 데이터 저장 / 변환해서 저장이 있어야 한다.

- 사용자 TABLE, MaintTable. 식별자ID / 생년 / 월 / 일 / 시 / IP / 본 시간

- MBTI 테이블(one to Many) - 사용자 테이블에 소속된다.

- 맞았는지 테이블(one to Many) - 사용자 테이블에 소속된다.

- 댓글 테이블(Many to Many) - 사용자 테이블에 소속된다.



# 필드 설명

- DateTimeField(auto_now=False, auto_now_add=False, **options)

    - TextInput이 기본 widget이다. auto_now를 쓰면 현재 시점이 저장이 되고, auto_now_add를 쓰면 

- null필드

    - `null=True`라면, 장고는 빈 값은 NULL로 저장한다. null을 CharField나 TextField에 넣지 말아라. string-based field에 null=True를 넣게 되면 데이터가 없을 때 2가지의 의미 값을 갖게 된다. "no data"를 2개의 의미로 갖는 것은 불필요하다. 장고는 empty string을 쓰기를 권장한다.

- CharField
    - CharField에서 `unique=True`이고 `blank=True`라면, unique의 규제를 피해 다양한 처리를 위해서 `null=True`여야한다.

- null은 database를 위한 것이고, 실제로 제출했을 시 입력값을 넣지 않는다고 나온다. `blank=True`로 설정해야지 from에 유지된다.
- Django will store empty values as NULL in the database. 

- GenericIPAddressField

    - TextInput위젯의 변형

- AutoField
    
    - id = models.AutoField(primary_key=True)


# 참조

[필드 설명](https://docs.djangoproject.com/en/2.2/ref/models/fields/)

[AutoIncrement](https://docs.djangoproject.com/en/1.11/topics/db/models/#automatic-primary-key-fields)

[ip필드 설정](https://stackoverflow.com/questions/41123659/django-ipv4-only-for-genericipaddressfield)