---
layout: post
title: Django 11 - App만들기
category: Django
tags: [python, Django]
comments: Django
---

### 앱 생성하기

- `django-admin startapp rooms`로 룸 어플리케이션을 만들 수 있다. 어플리케이션 이름은 **복수형**으로 하는게 좋다.

- 똑같이 users, reviews, conversations, lists, reservations을 만든다.

```console
django-admin startapp users
django-admin startapp reviews
django-admin startapp conversations
django-admin startapp lists
django-admin startapp reservations
```

- 사용자들(users) 방을보고(rooms) 예약(reservations)하는 웹. 방에 대해서 리뷰(reviews)를 남기거나, 좋아요(lists)누르거나, 호스트와 대화(conversations)를 할 수 있다.

- users : 회원정보를 담고 있다. 회원가입(깃허브, 카카오) / 로그인, 로그아웃 

- reviews : 사용자들이 방에 대해서 댓글을 남긴다. (사용자가 방에 대해서 예약을 한다.not host)

- rooms : 방의 정보를 담고 있다. ( 호스트가 존재한다. / 방의 타입, 편의시설, 규칙, 제공용품)

- reservations : 사용자들이 방에 대해서 리뷰를 남긴다. (사용자 하나 - 방 하나)

- conversations : 사용자들이 호스트와 대화하기 (사용자 하나 - 사용자 하나)

- 관리자 페이지에 들어가면 users탭이 있다. 그런데 새로운 user를 만든 이유는 user페이지가 장고 관리자용 페이지이기 때문이다.

- **실제 사용 유저들**만을 위한 분리된 admin창이 필요하다. 페이스북으로 로그인, 구글로 로그인 같은 것을 관리할 users application이 따로 필요하다.

### 장고 운영시 주의할 사항

- **파일 이름을 절대 변경해서는 안 된다**. framework를 쓰지 library를 쓰는 것이다. framework는 룰에 따라야 한다. library는 뭔가를 build하기 위해서 배운다. react는 라이브러리고 할 수 있다. 마음대로 변수명을 바꿀 수 있다. 반면 장고의 파일명, 변수명은 바꿀 수 없다.

- admin패널에서 users가 어떻게 보여질지를 변경하고 싶다면 코드를 작성하는 곳은 admin.py여야 한다.

- view를에다가 작성해야한다.

- 장고는 urls.py를 호출한다.장고는 urls.py를 url로서 로드한다.

- settings.py를 바꾸면 안 된다. 이름은 정해졌다!!! migrate명령어를 치면 django는 `migrations폴더에 있는 migration파일들`을 주시하게 된다!!!

- framework의 rule에 따라야한다. 장고에서 이름 바꾸면 절대 안돌아간다.

### 앱의 구성요소

- users어플리케이션의 **admin.py**에 어떤 코드를 넣던 Django의 **admin 패널에 반영**된다.

- apps.py는 구성요소이다. 별로 신경 안 써도 된다.

- Models는 Data이다. database가 어떻게 생겼는지 설명해주는 곳이다.

- views는 사용자에게 보여주는 render하는 function을 넣게 된다.

- config의 url.py는 전체 url을 콘틀로한다. 그런데 많은 파일이 있기 때문에 `users에 urls.py를 새로 생성`한다.

### 참고로 알아두면 좋은 사항

- tip : 컨트롤 키를 누르고 마우스를 누르면 해당 function의 정의 부분으로 갈 수 있다.


- 쟝고 위에 있는 코멘트들은 매우 중요하다. 예를 들어서 `# SECURITY WARNING: keep the secret key used in production secret!`이나 `# SECURITY WARNING: don't run with debug turned on in production!`의 경고 문구가 있다.

- 링크들도 중요하다. "https://docs.djangoproject.com/en/2.2/topics/auth/passwords/#password-validation"로 장고 문서를 참조할 수 있다. 아래에 설명서를 읽어보고 **소스코드**도 확인할 수 있다. **장고를 설치**할 때 이런것들이 다 함께 오게 된다.

```
UserAttributeSimilarityValidator, which checks the similarity between the password and a set of attributes of the user.
MinimumLengthValidator, which simply checks whether the password meets a minimum length.

This validator is configured with a custom option: it now requires the minimum length to be nine characters, instead of the default eight.
```


# 참고

