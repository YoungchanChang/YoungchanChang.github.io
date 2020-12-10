---
layout: post
title: spring 01. 프로젝트 생성
category: spring
tags: [spring]
comments: spring
---

# Maven Gradle 차이

- Maven과 Gradle의 차이 : 필요한 라이브러리 받고 관리하는 툴

- Gradle이 Maven보다 더 간결하게 구성 가능

# Thymeleaf

- Thymeleaf는 템플릿 엔진으로 스프링 프레임워크의 MVC 구조에서 V 즉, 뷰(View)를 담당하는 라이브러리

# Gradle파일

- Gradle파일의 역할 : 버전설정, 라이브러리 다운

- sourceCompatibility : 자바 버전

- repositoreis : 라이브러리 다운받는 저장소

- Junit5라는 라이브러리가 기본적으로 들어가 있다.

# 기타 파일

- .gitignore 깃에 저장하지 않게 해주는 파일

- resources에서는 자바파일을 제외한 나머지 파일. xml이나 properties같은 자바 설정파일이 존재

# 폴더

- .idea는 intellij 설정파일

- test폴더는 테스트 관련된 코드

# tip

- settings에 gradle칸에 "buiild and run using:"과 "Run tests using"을 IntelliJ로 바꾸면 IntelliJ에서 JAVA를 바로 띄워줌으로써 속도가 향상된다.