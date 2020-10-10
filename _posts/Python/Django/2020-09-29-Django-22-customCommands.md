---
layout: post
title: 파이썬 장고 CUSTOM COMMANDS AND SEEDING
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[django-admin commands](https://docs.djangoproject.com/en/2.2/howto/custom-management-commands/)

# django-admin commands 커스텀하기

- 장고에 내가 만든 명령어를 수행하게 하고 싶을 때 사용할 수 있다. 여기서는 데이터베이스에 dummy데이터를 넣을 때 사용할 수 있다.

- 장고의 규칙에 맞춰서 폴더를 만들고 코드를 작성해야한다.

- **내가 장고를 이용하는게 아니라 장고가 내 코드를 이용한다.**

### 나만의 `python manage.py commands` 만들기

- **어떤 argument를 전달**할 것인지, 해당 argument로 **무엇을 할 것인지** 명시해야한다.

- 어떤 argument를 전달할 것인지는 `def add_arguments(self, parser):`에 명시해야한다. 어떻게 다룰 것인지는 `def handle(self, *args, **options):`에 전달해야한다.

- 장고 seeds를 이용해서 가짜 데이터베이스를 빠르게 만들기

- 아무 폴더로 들어가서 폴더 만들기. 파일이름은 __init__.py

- 장고가 이 폴더가, 장고에게 파이썬 폴더라는 것을 알려준다. /rooms/management/__init__.py

- /rooms/management/commands/__init__.py, loveyou.py

- 에러 메시지 `AttributeError: module 'rooms.management.commands.loveyou' has no attribute 'Command'`가 뜬다.

- 에러메시지의 의미는 Command클래스를 기대한다는 의미이다.

- loveyou.py에 아래 파일 생성

- 에러메시지 `AttributeError: 'Command' object has no attribute 'run_from_argv'` 발생

- argument를 지운다.

- `NotImplementedError: subclasses of BaseCommand must provide a handle() method`에러 발생

- BaseCommand 내부로 들어가서 읽어본다!!!

- 읽다보면 아래와 같은 문구가 발생한다.

```python
    # Metadata about this command.
    help = ''

    #더 아래로
        def add_arguments(self, parser):
        """
        Entry point for subclassed commands to add custom arguments.
        """
        pass
```

- 아래와 같은 function을 쓸 수 있다.

```python
class Command(BaseCommand):
    print("hello")

    help = "This command tells me that he loves me"

    def add_arguments(self, parser):
        parser.add_argument(
            "--times", help="How many time do you wnat me to tell you that i love you?"
        )
```

- `python manage.py loveyou --help`명령어를 치면 아래와 같이 콘솔 명령어가 뜬다.

```console
optional arguments:
  -h, --help            show this help message and exit
  --times TIMES         How many time do you wnat me to tell you that i love
                        you?
```

- 문서를 읽으면 하위 클래스는 반드시 이 메소드를 구현해야 된다고 나온다.

```python
    def handle(self, *args, **options):
        """
        The actual logic of the command. Subclasses must implement
        this method.
        """
        raise NotImplementedError('subclasses of BaseCommand must provide a handle() method')
```

