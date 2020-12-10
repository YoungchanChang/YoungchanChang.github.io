---
layout: post
title: Django 05 - 파이썬 장고 구성확인
category: Django
tags: [python, Django]
comments: Django
---

# config확인하기

### 파일 별 기능

- `__init__.py`는 파이썬에 관련된 파일이다. 이 파일이 존재하는 디렉터리는 패키지의 일부임을 알려주는 역할을 한다. 해당 파일이 경로에 있어야 다른 파이썬 파일들을 import시켜서 쓸 수 있다.

- `settings.py`는 장고 프로젝트의 환경설정을 진행하는 부분이다.
    - 셋팅에서 TIME_ZONE = "UTC"을  TIME_ZONE = "Asia/Seoul"로 바꾸면 서버 시간은 서울기준이 된다.

- `manage.py`는 명령어 실행을 위한 유틸리티이다.

- `urls.py`는 장고 프로젝트의 URL을 선언하는 부분이다.

- `asgi.py, wsgi.py`는 웹서버에 호환가능한 시작점이다.

### __init__.py

- __init__.py말고도 파이썬을 다룰 수 있다. 

- 이 코드는 현재 스크립트 파일이 실행되는 상태를 파악하기 위해 사용

- __name__은 **모듈의 이름이 저장되는 변수**로써, 스크립트 파일을 **직접 실행했을 때는 __main__**이 실행

```python
if __name__ == '__main__':
    print(result_json)
```

# 참고

[장고 튜토리얼 file기능](https://docs.djangoproject.com/en/3.1/intro/tutorial01/)

[장고 URL](https://docs.djangoproject.com/en/3.1/topics/http/urls/)

[__name__](https://dojang.io/mod/page/view.php?id=2448)