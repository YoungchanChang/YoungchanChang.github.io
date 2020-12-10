---
layout: post
title: 웹스크래핑07. 서버의 개념
category: webscraping
tags: [python, server]
comments: python
---

# 클라이언트와 서버의 개념

- Client는 고객으로 서비스를 요청하는 사람이고, Server는 서비스에 대한 제공자이다. 

- 예를들어 맥도날드(Server)에서 고객(Client)는 주문요청(Request)을 하고 서버는 그것에 응답(Respond)을 한다.

- 웹 사이트의 경우 Client는 웹 사이트를 이용하는 사람이고, Server은 웹 사이트 운영자이다. 해당 서버는 집에 있는 컴퓨터로도 운영할 수 있다.

<center>
<figure>
<img src="https://imgur.com/jftnqZe.png" alt="views">
<figcaption>클라이언트의 요청에 응답한다.</figcaption>
</figure>
</center>


### 클라이언트의 특징

- 무조건 **요청(Request)**밖에 하지 못 한다.

- 클라이언트는 **주소창을 통해** 자신의 요청 목적을 명시한다.

### 서버의 특징

- 클라이언트의 요청에 맞는 적절한 **응답(Respond)**을 해준다.

- 서버의 응답의 형태는 다양하다. "빅맥주세요"하는데 빅맥을 주는 것도 응답이지만, **무응답이나 거절**도 응답이다.


### 클라이언트 요청 구문 분석

- 네이버에 화요일 웹툰을 요청할 때 구문은 아래와 같다.

```
(https://comic.naver.com:80/webtoon/detail.nhn?titleId=683496&no=164&weekday=tue)
```

- 이것을 URL : Uniform Resource Locator이라고 부른다.

- URL구조 분석

```
1. https:// - 프로토콜. 서버에 어떻게 정보를 줄 것인지 규칙을 정의한다.
2. //comic.naver.com - 도메인. 인터넷 통신은 IP주소를 이용하는데 사람이 기억하기 어려움으로 문자로 바꿔주는 역할을 한다.
3. :80 - 포트번호. 컴퓨터 안에 세부 통신 주소를 의미한다. IP가 아파트라면, 동, 호수는 포트번호이다.
4. / - 루트를 의미. 웹 루트 디렉터리를 의미한다.
5. webtoon/ - 폴더명으로 웹 루트 디렉터리 아래에 있는 폴더를 의미한다.
5. /detail.nhn - 실제 서버가 돌려주는 파일을 가리킨다.
6. ?titleId=683496&no=164&weekday=tue - URL을 통한 get방식으로, 파일 요청 시에 추가로 주는 인자값(parameter)이다. KEY=VALUE구조로 전달되며 여러개를 쓰고싶을 경우 &를 쓰게 된다.
```