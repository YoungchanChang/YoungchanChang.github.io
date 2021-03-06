---
layout: post
title: javascript-14 OOP
category: javascript
tags: [javascript, OOP]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6553)강의를 요약, 정리한 글입니다.  

# 객체지향

### 객체지향이란?

- 로직을 상태(state)와 행위(behave)로 이루어진 **객체**로 만드는 것으로 **레고 블럭처럼 조립해서 하나의 프로그램을 만드는 것**이 객체지향 프로그래밍이다.

### 왜 객체지향을 쓰는가?

- 객체지향을 사용하면 코드의 양을 극적으로 줄일 수 있고, **객체 별로 기능이 분류**되어 있기 때문에 필요한 코드를 찾기도 쉽고 문제의 진단도 빨라진다.

### 어떻게 객체로 만드는가?

1. 부품화

- 연관된 메소드와 그 메소드가 사용하는 변수들을 분류하고 그룹핑한다.

2. 은닉화 : 캡슐화

- 중요한 **데이터를 보존,보호하기 위해 사용**하는 것이다

- 멤버 변수 앞에 접근 제어자 private를 붙인다. (private: 자기 클래스에서만 접근할 수 있는 것 )

- 멤버 변수에 값을 넣고 꺼내 올 수 있는 메소드를 만든다 (접두어 set/get을 사용해 메소드를 만든다.)

3. 그 밖에 상속, 다형성, 추상화도 있다.

# 참조
[자바 은닉화](https://mainpower4309.tistory.com/7)