---
layout: post
title: Django 02 - 파이썬 가상환경 pip설치하기
category: Django
tags: [python, Django]
comments: Django
---

# Pycharm 사용시 pipenv 사용하기

- 우측 하단의 Interpreter클릭 => Add Interpreter클릭 => Pipenv Environment 클릭 => Interpreter 클릭

# Pycharm 가상환경

- PyCharm의 가상환경은 우측 하단에 존재한다.

- 그런데 만약 python_version이 바뀌거나 하면 패키지를 재설치하는데 불편함이 생긴다.

# vscode에서 pipenv사용

- 아래 명령어 입력

```console
pipenv --three
pipenv shell
pipenv install Django==2.2.5
django-admin
```

# 파이참의 장점

- vscode에서 설치해서 운영했을 때, Ctrl + 클릭 등으로 자세히 보기 기능이 지원되지 않았다.

- 변수명 자세히 보기와 디버그 기능의 편리함으로 파이참을 쓰면 편리

- 내가 써 본 결과 VSCODE에 비해서 디버그 기능이 편리하다. 우측 상단에서 디버깅이나 run을 둘 다 할 수 있다.

- 하단의 깃허브 시각화가 잘 되어있다. 브랜치나 이전 기록들도 잘 보인다.