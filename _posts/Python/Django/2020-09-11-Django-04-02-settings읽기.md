---
layout: post
title: 파이썬 장고 setting.py설정
category: Django
tags: [python, Django]
comments: Django
---

# settings내용 읽기

- `import os`는 os의 모듈에 정보를 가져올 수 있다. 몇 bit를 쓰는지, 플랫폼은 윈도우인지 리눅스인지, 이름은 뭔지에 대한 정보가 들어있다. 시스템의 정보를 통해서 

# 배포시 고려할 사항

- 로컬로 돌릴때와 실제 배포때는 차이가 있다. HTTPS, 캐싱, 에러 보고는 개발할 때는 불필요하다.

- 신경써야 될 부분 보안 수준, 다른 환경, 보안 특성, 성능 최적화, 에러 리포팅

- `python manage.py check --deploy`명령어를 입력하면 WARNING들이 뜬다.

```
WARNINGS:
?: (security.W004) You have not set a value for the SECURE_HSTS_SECONDS setting. If your entire site is served only over SSL, you may want to consider setting a value and enabling HTTP Strict Transport Security. Be sure to read the documentation first; enabling HSTS carelessly can cause serious, irreversible 
problems.
```

### SECRET_KEY

- SECRET_KEY는 하드코딩 하지 말아야 한다. envorinment variable이나 file에서 불러와야한다.(dotenv를 이용하면 된다.)

- SECRET_KEY의 용도

```python
import os
SECRET_KEY = os.environ['SECRET_KEY']

OR

with open('/etc/secret_key.txt') as f:
    SECRET_KEY = f.read().strip()
```

# DEBUG

- `DEBUG = True`로 하지 말아야 한다. 프로젝트에 대한 많은 정보들이 센다.

### ALLOWED_HOSTS

- `DEBUG = False`가 된다면, 장고는 ALLOWED_HOSTS없이 움직이지 않는다. CSRF공격으로 부터 보호해야한다.

- 서버는 불필요한 요청에 대해서 static error page나 request를 막아야 한다. 그래야 장고 로그에 불필요한 로그가 쌓이지 않는다.

### CACHES

- 장고는 로컬 메모리 캐싱을 기본적으로 쓴다.

### DATABASES

- DB패스워드에 대해서 신경써야한다.

# 참고

[셋팅](https://docs.djangoproject.com/en/2.2/ref/settings/)

[참고](http://pythonstudy.xyz/python/article/507-%ED%8C%8C%EC%9D%BC%EA%B3%BC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC)