---
layout: post
title: javascript-15 prototype
category: javascript
tags: [javascript, prototype]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6573)강의를 요약, 정리한 글입니다.  

- javascript는 **prototpye based language**라고 할 만큼 프로토타입은 javascript에서 매우 중요한 개념이다. 객체, 함수와의 관계에서 prototype은 의미가 있다.

# prototype

### prototpye이란?

- prototype은 객체의 원형이다. prototype이라는 프로퍼티는 용도가 약속되어있는 **특수한 프로퍼티**이다. 프로퍼티에 **저장된 속성**들은 생성자를 통해서 객체가 만들어질 때 **그 객체에 연결**된다.

<center>
<figure>
<img src="https://imgur.com/IE7kYXL.png" alt="views">
<figcaption>프로퍼티는 특수한 객체이다.</figcaption>
</figure>
</center>


### prototype chain - 프로토타입이 앞의 프로토타입을 가리키는 것을 의미하는 용어

- prototpye이란 도대체 무엏일까? **생성자는 기본적으로 함수**이다. 앞에 new를 붙이면 생성자로써 역할한다. 새로운 객체를 만들어서 해당 객체를 return하기 때문에 o라는 변수 안에는 생성자를 통해 만들어진 객체가 들어간다.

### prototype는 객체와 객체를 연결하는 체인의 역할을 하는 것
1. 객체 o에서 ultraProp를 찾는다.
2. 없다면 Sub.prototype.ultraProp를 찾는다.
3. 없다면 Super.prototype.ultraProp를 찾는다.
4. 없다면 Ultra.prototype.ultraProp를 찾는다.

- 상속받고자 하는 객체의 복제본을 사용해야한다. prototpye하면 부모객체에도 영향을 미칠 수 있다.

- [자바스크립트 자료 시각화](http://pythontutor.com/visualize.html#mode=display)를 참조하자.
- [javascript OOP]()에서 객체지향에 상속의 개념이 들어간다.