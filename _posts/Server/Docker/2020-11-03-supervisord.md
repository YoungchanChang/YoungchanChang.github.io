---
layout: post
title: supervisord
category: server
tags: [python, server]
comments: server
---

# 슈퍼바이저

supervisord : 프로세스를 daemon으로 위탁관리해주는 tool이다.

nohup명령어을 통해서 백그라운드 프로세스를 실행시킬 수 있음.
툴을 사용하면, restart를 하거나 로그등의 관리를 손 쉽게 할 수 있음


# 슈퍼바이저 팁

- 슈퍼바이저랑 gunicorn을 사용해야 하는 경우에 가상환경까지 설치해서 진행해야 하는 경우가 있다. 그럴 때 아래와 같이 수행하면 된다.

```
source /home/user/.virtualenvs/my_venv/bin/activate     ; 파이썬 가상환경 활성화
cd /home/user/myapp     ; 프로그램 디렉터리로 이동
exec /home/user/.virtualenvs/my_venv/bin/gunicorn -b 0.0.0.0:8081 myapp.wsgi:application     ; 가상환경에 설치된 gunicorn 실행
```

SUPERVISORD
[참고](https://devlog.jwgo.kr/2016/11/07/how-to-use-supervisor-in-one-minute/)

GUNICORN
[장고 & Gunicorn 연동](https://ossian.tistory.com/110)

[장고 & nginx](https://yujuwon.tistory.com/entry/%EC%9A%B0%EB%B6%84%ED%88%AC%EC%97%90%EC%84%9C-Django%EC%99%80-gunicorn-supervisor-nginx-%EC%97%B0%EB%8F%99-%ED%95%98%EA%B8%B0)

requirement
[참고](https://itholic.github.io/python-requirements/)

# 슈퍼바이저 실습

[간단한 실습](https://yongbeomkim.github.io/django/supervisord-ctl/)

[두번째 실습](http://www.kwangsiklee.com/2018/12/supervisord-%EC%82%AC%EC%9A%A9%EB%B2%95%EC%9D%84-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90/)

- service supervisor start
- servics supervisor status


# 슈퍼바이저 관련 에러

> [참조](https://stackoverflow.com/questions/49952742/error-cant-reread-the-directory-named-as-part-of-the-path-home-app-logs-celer)

- 에러코드
(ERROR: CANT_REREAD: The directory named as part of the path /home/my_username/test_process_output.txt does not exist. in section 'program:test_process' (file: '/etc/supervisor/conf.d/test_process.conf'))

- 디렉터리가 제대로 있는지 확인할 것





- 엘라스틱서치도 항상 수행되어있어야함

- supervisorctl로

- /home/bokji_qa

- 아래 내용 추가

- 슈퍼바이저 설치

$ sudo apt-get install supervisor

- /etc/supervisor/conf.d/run.conf 을 생성

# 내가 짠 코드

```
[program:bokji_python_process]
command=gunicorn3 bokji_main_server:app -b 0.0.0.0:9101 -m 3
directory=/home/bokji_qa
user = root
autostart = true
autorestart = true
redirect_stderr=true
```

# 확인

- apt-get install net-tools

-  netstat -ntlp | grep :9100

service supervisor start

service supervisor status

엘라스틱 이슈 Elasticsearch memory problems
[자료](https://stackoverflow.com/questions/29447434/elasticsearch-memory-problems/40657077)


requiremnets 팁

[https://itholic.github.io/python-requirements/]


대환장 에러파티
- pip install --upgrade pip setuptools==45.2.0
[setuptools](https://www.programmersought.com/article/26594738779/)

- Could not find a version that satisfies the requirement keras-contrib==2.0.8


[해결](https://stackoverflow.com/questions/49791178/importerror-no-module-named-keras-contrib)


tail -f bokji_python_process

???

ERROR (spawn error)