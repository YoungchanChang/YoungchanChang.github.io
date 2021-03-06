---
layout: post
title: Django 04 - 파이썬 장고 VScode setup
category: Django
tags: [python, Django]
comments: Django
---

# 장고 설치

- 튜토리얼에 나와있는대로 `$ django-admin startproject mysite` 명령어로 장고 프로젝트를 구성했을 때 불편함이 많다.

- mysite디렉터리 안에 manage.py파일이 존재함으로 매번 1-depth를 들어가서 명령어를 수행해야 된다.

- 또한 최상위에 위치하지 않으면 규모를 확장하거나 여러 개발자와 협업을 할 때 불편함이 있다.

### 장고설치

1. `$ django-admin startproject config`로 프로젝트를 생성한 뒤에 config폴더 이름을 Aconfig로 바꾼다.

2. Aconfig 안에 있는 config폴더와 mange.py를 바깥으로 꺼낸다.

- python에서는 **django-admin은 관리용 유틸리티 명령어 라인**이다. 약간 sudo su같은 느낌인다.

- **manage.py는 django-admin과 같은 역할**을 하고, settings.py를 다룰 때 사용한다.

- 바깥으로 꺼내는 이유는 경로를 조금 더 다루기 쉽게 만들기 위함이다.

### 장고 추가 설치

- vscode Extenstion에서 python, flake8, pylint를 설치하면 코드를 관리하는데 도움이 된다.

- vscode에서 python을 설치하면 좌측 하단에서 interpreter을 확인할 수 있다. python interpreter버전을 확인할 수 있다.

### flake8과 Linter의 역할, formatter

- 파이썬은 컴파일 언어가 아닌 **런타임 언어**로써 컴파일러가 프로그램이 시작되기 전에 에러를 잡아주지 않는다.

- Linter은 내가 쓴 코드를 보면서 **에러가 생길 부분을 미리 감지**하는 것이다. 예를들어 변수를 만들었는데 사용되지 않거나, 선언되지 않은 변수를 사용할 경우 문제를 명시한다.

- Linter은 또한 python convention도 준수하려고 한다. **python pep**을 보면 pep8에 style가이드가 나온다. 배치, fucntion을 얼마나 띄우고 마지막 공간을 얼마나 줄지. Linter은 가이드라인을 따라할 수 있게 도와준다.

- flake8은 Linter의 한 종류이다. linter과 flake8 둘 다 문법적으로 도와주는 툴이다.

- `pipenv install flake8 --dev`로 설치가 된다. 설치를 하면 pipfile에 [dev-packages]부분에 flake8="*"로 추가되어있다. [dev-packages]는 개발할 때만 필요한 패키지이다.

- formatter는 코드를 보기 좋게 자동으로 수정해준다. 사용하는 foramtter은 black이다. `pipenv install black --dev --pre`

- Ctrl + S를 누르면 하단에 Formatting with black이라고 매우 빠르게 생긴다.

- 추가로 Manage에 setting에 들어가서 format on save로 자동 수정을 확인한다.

- vscode설정파일에 들어가서 아래와 같은 설정이 있는지 확인한다.

# 설정 파일

- flake8설치됨, pylint끔(flake가 대신함), formatter black으로 설치함. (자동 수정 확인)

```
{
    "python.pythonPath": "C:\\Users\\msi\\.virtualenvs\\1thefull-q8RE0l9b\\Scripts\\python.exe",
    "python.linting.flake8Enabled": true,
    "python.linting.pylintEnabled": false,
    "python.linting.enabled": true,
    "python.formatting.provider": "black"
        "python.linting.flake8Args": [
        "--max-line-length=88"
    ]
}
```

# 참고

[장고 프로젝트 시작](https://docs.djangoproject.com/en/3.1/intro/tutorial01/)

[장고 admin의 역할](https://docs.djangoproject.com/en/3.1/ref/django-admin/)