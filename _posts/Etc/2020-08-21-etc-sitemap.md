---
layout: post
title: 구글 검색엔진에 내 블로그 등록하기
category: etc
tags: [etc, google, robot.txt, sitemap.xml]
comments: true
---

> 사람들이 구글에서 내 사이트를 검색해서 들어올 수 있게 하는 방법을 알아봅니다.

## 1. 구글 검색엔진(웹마스터 도구)에 내 사이트 등록하기

1. [구글 웹마스터 도구](https://www.google.com/webmasters/tools/)에 접속합니다.
2. 속성 유형 중 우측의 URL 접두어에 자신의 URL입력(https://youngchanchang.github.io/)합니다.
3. 소유권 확인 방법 중 HTML파일을 클릭해서 다운로드합니다.
4. 루트 디렉터리에 해당 파일을 넣고 깃허브에 commit&push를 한 뒤 인증버튼을 누릅니다.
5. 만약 등록했는데도 인증이 되지 않으면서 "필요한 위치에서 확인 파일을 찾을 수 없습니다"라고 나올 경우 다른 확인 방법의 HTML 태그 방법을 씁니다.(나의 경우는 계속 인증이 안 되서 HTML태그 방법을 쓴 뒤 시간이 조금 지나니깐 됬다.)

## 2. 로봇.txt 파일 생성

> 검색 엔진의 크롤러라는 로봇이 여러 사이트들을 돌아다니면서 정보를 수집한 후 검색 엔진에 제출합니다.
> 크롤러가 내 사이트의 정보를 검색해도 된다는 명시를 하는 파일이 robot.txt파일입니다.

1. 자신의 블로그의 루트 디렉터리에 robot.txt파일을 생성합니다.
2. 아래 코드를 붙여넣습니다.

```
User-agent: *
Allow: /
Sitemap: http://[자신의 github 사용자명].github.io/sitemap.xml
```


## 3. sitemap.xml 파일 작성

> sitemap.xml은 크롤러가 사이트에 접속했을 때 사이트를 정확하고 효율적으로 탐색할 수 있게 합니다.


1. 블로그의 루트 디렉터리에 sitemap.xml파일을 작성합니다. 내용은 [여기](<https://joelglovier.com/writing/sitemaps-for-jekyll-sites>)를 참조합니다.
2. 루트 디렉토리에 존재하는 _config.yml파일 내의 url 부분에 자신의 블로그 url을 입력합니다.
- 유틸리티 레이아웃(feeds 같은 경우)는 없애야합니다.
3. 마지막으로 깃허브에  commit&push를 합니다.


## 4. 구글 웹마스터 도구(Search Console)에 sitemap.xml 제출
1. [구글 웹마스터 도구](https://www.google.com/webmasters/tools/)에 접속합니다.
2. 좌측 상단에 내가 등록한 사이트 선택합니다.
3. 왼쪽 메뉴 중 색인 > Sitemaps 선택합니다
4. 새 사이트맵 추가에 깃허브에 등록한 /sitemap.xml 제출합니다.

# 참조글
- <https://joelglovier.com/writing/sitemaps-for-jekyll-sites>
- <https://gmlwjd9405.github.io/2017/10/20/include-blog-in-a-GoogleSearchEngine.html>
- <https://www.youtube.com/watch?v=xGkftwkoJK4>

