---
layout: post
title: 파이썬 장고 User Uploads part One
category: Django
tags: [python, Django]
comments: Django
---

# 장고가 request를 처리하는 방법

- 장고에 URL요청을 날렸을 때, 파이썬 코드는 아래와 같이 실행된다.

- 1.장고는 `ROOT_URLCONF`셋팅에 간다.

- 2.장고는 `urlpatterns`변수를 통해 파이썬 모듈을 불러온다. jdango.urls.path()나 django.urls.re_path()여야 한다.

- 3.장고는 각 URL패턴을 찾아다니며 **첫번째로 맞는 requesteURL에 매칭**한다.

- 4.URL패턴이 매치되면, 장고는 view를 반환한다.

- 5.만약 매칭되는게 없다면 적절한 error를 반환한다.

### 에러 핸들링

# 참고

[MEDIA_ROOT](https://docs.djangoproject.com/en/2.2/ref/settings/)

[에러코드 해결책](https://has3ong.tistory.com/238)

[URL_patterns](https://docs.djangoproject.com/en/2.2/ref/urls/#django.urls.path)

[에러 핸들, dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/#error-handling)