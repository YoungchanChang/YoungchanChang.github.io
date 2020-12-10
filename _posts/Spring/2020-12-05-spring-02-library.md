---
layout: post
title: spring 02. 라이브러리 살펴보기
category: spring
tags: [spring]
comments: spring
---

# 라이브러리와 프레임워크의 차이

- 프레임워크는 내 코드를 쓰고, 나는 라이브러리를 쓴다.

# 스프링부트 라이브러리

- 프레임워크를 구성하는 라이브러리 목록

### spring-boot-starter-web : 서버 관련된 라이브러리

- spring-boot-starter-tomcat: 톰캣 (웹서버)
- spring-webmvc: 스프링 웹 MVC

### spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)
- spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
- spring-boot
- spring-core
- spring-boot-starter-logging
- 로그와 관련된 라이브러리 logback, slf4j를 보면 된다.

# 테스트 라이브러리
### spring-boot-starter-test
junit: 테스트 프레임워크
mockito: 목 라이브러리
assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
spring-test: 스프링 통합 테스트 지원

# TIP

- 실제 라이브러리를 써 봐야 안다. 따라서 실제 라이브러리를 쓸 때 이 목록을 보자.