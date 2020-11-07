---
layout: post
title: add-apt-repositor
category: linux
tags: [linux]
comments: linux
---

> [참고](https://wnw1005.tistory.com/365)


- add-apt-repository란?

`apt-get install package`로 패키지를 설치하면 되는데 왜 굳이 add-apt-repository명령어를 수행할까?

add-apt-repository ppa:fkrull/deadsnakes

#

- `apt-get install package`명령어로 공식저장소에 설치된 패키지를 설치할 수 있다.

- 공식 저장소는 안정성과, 검증된 패키지를 오리기 때문에 최신 버전이 아닐 수 있다.

- 때로는 공식 저장소에서는 지원하지 않는 패키지가 필요할 때가 있다. 최신 버전이 필요한 경우나 기존의 공식 개발 팀이 배포한 패키지의 개인적인 버그 수정이나 기능 개선 등 특정 목적으로 패키지를 수정해 재배포할 때 쓸 수 있다.
