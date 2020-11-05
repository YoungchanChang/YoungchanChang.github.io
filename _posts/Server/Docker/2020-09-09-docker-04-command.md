---
layout: post
title: Docker 04. 도커의 기본 명령어(ps, stop, rm, logs, images, ... )
category: docker
tags: [docker]
comments: docker
---

# Docker

- 실행중인 컨테이너 목록 확인 : ps
- 도커 중지하기 : stop, rm
- 도커 로그 확인하기 : logs
- 다운받은 이미지 보기 : images
- 컨테이너 디렉터리와 실제 디렉터리 연결 옵션 : -v

### 실행중인 컨테이너 목록 확인

- 실행중인 컨테이너 목록 확인

```
docker ps
```

- 중지된 컨테이너도 확인할 수 있다.

```
docker ps -a
```

### 도커 중지하기

- 실행중인 컨테이너 중지하기. 띄어쓰기로 여러개 중지할 수 있다.

```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

- 종료된 컨테이너 완전히 제거하기. 찌꺼기가 남아있을 수 있다.

```
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

### 도커 로그 확인하기

- 컨테이너 띄우고 에러났을 때 로그를 봐야한다.

- `-f`옵션은 대기하면서 추가적인 로그가 생기면 보여준다.

```
docker logs [OPTIONS] CONTAINER
```

### 도커가 다운받은 이미지 보기

- 이미지가 없으면 컨테이너가 실행될 때 다운로드를 받는다.

```
docker images [OPTIONS] [REPOSITORY[:TAG]]
```


### 도커 -v옵션

- mysql을 멈췄다가 다시 실행해서 새로고침하면 DB접속에 실패했다고 나온다. mysql은 DB가 생성했을 때 데이터가 사라진다.

- 컨테이너가 가상에 생성된 데이터가 컨테이너 종료될 때 같이 사라진다.

- -v 옵션 : 내 실제 디렉터리를 컨테이너의 디렉터리와 연결해주겠다.

- 실제 mysql데이터가 저장되는 곳을 연결해준다.

```
docker stop mysql
docker rm mysql
docker run -d -p 3306:3306 \
 -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
 --network=app-network \
 --name mysql \
 -v /Users/subicura/Workspace/github.com/subicura/docker-guide/ch02/mysql:/var/lib/mysql \
 mysql:5.7
```

# 참고

[도커 툴박스](https://github.com/docker/toolbox/releases)

[도커 공식문서](https://docs.docker.com/toolbox/toolbox_install_windows/)

[도커 subicura](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)

[도커 툴박스 참조](https://jinyes-tistory.tistory.com/8)

