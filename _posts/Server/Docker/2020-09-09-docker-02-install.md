---
layout: post
title: Docker 01. 도커의 설치
category: docker
tags: [docker]
comments: docker
---


# 도커 설치시 유의 사항

- 도커는 기본적으로 linux위에서 돌아가기 때문에 Window설치 시 가상머신을 이용해야한다.

# 도커 설치


1. 윈도우의 작업관리자 `ctrl + alt + del`을 누른 뒤 작업관리자 > 성능 > CPU에 가상화 사용인지 체크

2. 기본값설정해서 시행

3. 바탕화면에 Oracle VM VirtualBox, Kitematic(Alpha), DockerQuickstart Terminal 3개가 생성되어있음

4. DockerQuickstart Terminal실행

5. 아래와 같은 메시지가 뜨면 다운로드 중인 상황

```
Running pre-create checks...
(default) Default Boot2Docker ISO is out-of-date, downloading the latest release...
...
Docker is up and running!
```

6. 명령어 입력 

`docker run hello-world`

7. 도커 설치 확인 `docker-version`
    - 클라이언트와 서버정보가 같이 나온다. docker환경에서는 명령어를 입력하는 클라이언트가 되고, 로컬 호스트의 도커라는 서버가 있다. 도커 자체가 Client-Server 구조가 된다.


# 에러메시지

(Docker Desktop requires Windows 10 Pro/Enterprise (15063+) or Windows 10 Home (19018+).)

원인 : Window 10 Home 에디션이 Hyper-V (윈도우 서버 가상화를 하지 않기 때문) 

해결책 : Toolbox로 깐다.


# 참고

[도커 툴박스](https://github.com/docker/toolbox/releases)

[도커 툴박스 공식문서 설치](https://docs.docker.com/toolbox/toolbox_install_windows/)

[도커 툴박스 참조](https://jinyes-tistory.tistory.com/8)