---
layout: post
title: Docker 01. 도커의 개념
category: docker
tags: [docker]
comments: docker
---

# Docker

### 도커의 개념

- 오픈소스 가상화 플랫폼 

- 예를 들면 리눅스에 MySQL서버를 실행한다고 했을 때, 기존 서버와 달리 도커라는 가상화 플랫폼을 이용해서 실행할 수 있게 된다.

```
기존의 동작 방식 : 리눅스 -> MySQL
도커의 동작 방식 : 리눅스 -> 도커(이미지 다운로드 받고 실행) -> MySQL(컨테이너)
```


- 컨테이너 : 격리된 환경에서 작동하는 **프로세스**. 리눅스 커널의 여러 기술을 활용. 하드웨어 가상화 기술보다 가벼움. **이미지 단위**로 프로세스 실행 환경 구성.


### 도커의 등장 배경

- 컨테이너는 애플리케이션을 환경에 구애 받지 않고 실행할 수 있게 해준다.(하나의 **표준화**된 작업 환경을 제공한다)
	- 리눅스 서버가 CentOS이건, Ubuntu이건 상관 없이 똑같은 명령어로 실행할 수 있게 된다.

- 서버를 **코드로 구성하고 관리**하기가 쉬워진다.
    - A와 B서버가 똑같은 구성을 했다고 하더라도, 라이브러리나 추가된 기능을 반영하다보녀 A와 B의 서버는 똑같이 않게 된다.
이런 상황에서 버그가 생긴다면 A와 B의 차이를 알아야 하는데 쉽지 않다. A와 B의 구성을 알고 같게 하기 위해 워드등을 이용해 **문서화** 할 수 있다. 혹은 환경설정은 어떻게 했는지 어떤 것이 바뀌었는지 **코드로 관리**할 수 있다.

- 도커의 장점 : 확장성 / 이식성
    - 도커가 설치되어 있다면 어디서든 컨테이너를 실행할 수 있음
    - 쉽게 개발서버를 만들 수 있고 테스트서버 생성도 간편함


- 도커는 이런 **코드화를 도와주는 도구**로써 이미지라는 것을 이용한다. 이미지는 게임 CD에 비교할 수 있다. 게임을 CD-ROM을 통해 구동하면 누구나 똑같이 게임이 실행된다. 여기서 게임을 진행하면서 저장을 하게 된다면 게임마다 상태가 달라지게 된다. 도커 이미지는 게임 CD와 같이 도커에 올리기만 하면 구동될 수 있는 파일을 의미한다.

- 이런 이미지 덕분에 도커는 1년전에 만든 파일을 1년전에 실행하나 오늘 실행하나 차이가 없게 된다.


### 참조 - 서버 관리를 위한 다양한 방법들

- **서버가 다운되지 않기 위해**서 인프라 관리자들이 굉장히 노력했다. 서버가 다운되면 안 되고, 업데이트가 쉬워야된다.

- 문서 관리

    - 어떤 명령어 입력했는지 문서화한다.

    - 단점 : 문서가 작성된 시점이나 OS가 다르면 똑같이 실행이 되지 않을 수 있다.

- 코드 관리

    - 사람이 명령어 입력하 듯이 코드로 관리할 수 있게 된다.

    - 단점 : 아파치 1.1과 아파치 1.2를 똑같은 서버에서 돌리고 싶을 때, 버전마다 경로, 설정을 다르게 해줘야 하는 어려움이 있다.

- 가상머신

    - 서버의 상태를 이미지로 저장한 뒤 가상머신에서 동작시킨다. 가상머신에서 cpu, 메모리를 할당해서 동작시킨다.

    - 단점 : 최종적인 결과는 보장되는데 어떤 식으로 만들어졌는지 모른다. 누군가 만든 것을 처음부터 다시 셋팅하려면 처음 만든 사람의 정보를 알아야 된다. 용량이 커서 공유도 힘들다. 가상머신이기 때문에 운영하는데 속도 저하가 있다. 

- 자원격리

    - **프로세스를 가상으로 분리**한다. 어떤 벽같은 것을 둬서 가상으로 서로 안겹치게 분리한다. 파일, 디렉터리도 가상으로 분리할 수 있다. CPU, MEMORY, I/O를 그룹별로 제한할 수 있다.

    - 단점 : 기술을 쓰기 어렵다


### 도커를 사용할 이유

- 도커를 사용하는 이유 : 윈도우에서 리눅스 서버가 구동하는 것과 같은 서버 환경을 구성해볼 수 있다. 그리고 내 코드를 적용시켜 본 뒤에 테스트 서버에 올릴 수 있다. 빌드 과정또한 관리가 된다.


# 참고

[도커 사용하는 이유](https://www.44bits.io/ko/post/why-should-i-use-docker-container)
[도커 장점](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)