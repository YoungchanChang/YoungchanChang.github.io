---
layout: post
title: 파이썬 가상환경 pip설치하기
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[pipenv](https://docs.pipenv.org/)

[ven사용 이유](https://www.daleseo.com/python-venv/)

[pipenv사용](https://medium.com/@erish/python-pipenv-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-961b00d4f42f)


# pipenv

### pipenv란

- pipenv는 **파이썬을 위한 npm + package.json**이다. 패키지 관리 툴(composer, npm, cago, yarn)의 역할을 한다.

### pipenv의 필요성

- pip는 패키지 관리 툴이다. **pip는 패키지를 global로 설치한다**. 그렇게 되면 PC내의 모든 프로젝트에서 운영체제에 설치된 하나의 파이썬 런타임을 사용하게 되고 프로젝트별로 충돌이 생길 수 있다. 비슷한 역할을 하는 것은 npm이다.

- 예를 들어 A프로젝트에 a패키지 1.1버전을 사용한다고 하자. 그리고 B프로젝트에서 a패키지 1.2버전이 필요해서 a패키지를 업그레이드 했다.그런데 a패키지 1.1과 1.2버전의 명령이 다르다고 했을 때, A프로젝트에서는 a패키지의 버전이 다름으로 오류가 생기게 된다.

- pipenv는 프로젝트에서 버블을 생성한다. **buble에다가 패키지를 설치**하니깐 global로 설치되지 않는다.

### pipenv설치하기

- `pip install pipenv`로 가상환경 설치한다. 여기서 주의할 점은 홈페이지에서 지원되는 python버전을 확인해야 된다. 나는 윈도우에서 3.8최신버전으로 파이썬을 설치했다가 오류가 생겨서, 3.7버전으로 낮춰서 진행됬더니 제대로 됬다.

- 실행하고자 하는 프로젝트에 들어간다.

- `pipenv --three` 명령어 치면 가상환경이 설정되면서 pipfile이 생성된다. --three옵션은 python3버전을 쓰겠다는 것이다. 그리고 생기는 pip파일안에는 어떤 패키지들이 설치되어있는지 명시되어 있다. package.json파일과 같은 것이다.

```
Successfully created virtual environment!
Virtualenv location: C:\Users\msi\.virtualenvs\Django-TcpgY73D
Creating a Pipfile for this project…
```

### 가상환경(bubble)에 장고 설치하기

- `pipenv shell` 버블 안으로 들어간다. 가상환경의 내부에 들어가서 뭔가를 설치할 수 있게 된다.

```
Launching subshell in virtual environment…
Windows PowerShell
```

- 가상환경 안에 들어가 있게 된다.

- `pipenv install Django==2.2.5` pipfile에서 packages부분에 django가 확인된 것을 볼 수 있다.

- `django-admin`명령어를 치면 여러 문구가 출력되야한다.

### BubbleTest

- `pipenv shell`로 가상환경으로 들어가지 않으면 `django-admin`명령어를 쳐도 아무런 반응이 없다.

- `pipenv shell`명령로 들어가면 'django-amdin'을 쳤을 때 작동이 된다.

- 버블의 바깥과 내부의 차이 : 프로젝트에서 Django로 뭔가를 하려면 먼저 pipenv shell부터 실행해야 된다.

### 깃에다가 올릴때 주의할 점

- `gitignore python` 검색해보면 파이썬 프로젝트에서 일반적으로 깃헙에서 올리지 않는 파일들이 나온다.

- `C:\Users\msi\.virtualenvs`의 경로에서 가상환경을 관리해주고 있다.

