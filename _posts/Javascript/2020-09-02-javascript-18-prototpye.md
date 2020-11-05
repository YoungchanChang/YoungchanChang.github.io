---
layout: post
title: javascript-18 prototype
category: javascript
tags: [javascript, prototype]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6573)강의를 요약, 정리한 글입니다.  

- javascript는 **prototpye based language**라고 할 만큼 프로토타입은 javascript에서 매우 중요한 개념이다. 객체, 함수와의 관계에서 prototype은 매우 의미가 있다.

# prototype

### prototpye이란?

- prototype은 객체의 원형이다. 객체는 프로퍼티로 값을 갖는데 prototype이라는 프로퍼티는 용도가 약속되어있는 **특수한 값**이다. 프로퍼티에 **저장된 속성**들은 생성자를 통해서 객체가 만들어질 때 **그 객체에 연결**된다.

### prototype을 쓰는 경우

- [javascript 상속]() 참조

<center>
<figure>
<img src="https://imgur.com/IE7kYXL.png" alt="views">
<figcaption>프로퍼티는 특수한 값을 가리킨다.</figcaption>
</figure>
</center>

### prototype활용 예시

- Ultra()객체를 Super()객체가 상속받고, Super()객체는 Sub()객체가 상속받는다. 결국, Sub()객체는 원형을 갖고 있게 된다.

- **생성자는 기본적으로 함수**이다. 함수로 만들어진 객체를 이용하여 값을 할당할 때 **new 키워드를 붙이면 해당 객체가 생성자로써 역할**한다. 새로운 객체를 만들어서 해당 객체를 return하면 o라는 변수 안에는 생성자를 통해 만들어진 객체가 들어간다.

```javascript
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
Super.prototype = new Ultra();
 
function Sub(){}
Sub.prototype = new Super();
 
var o = new Sub();
console.log(o.ultraProp);
```

### 반드시 알아야할 사항

- prototype chain의 개념

- 프로토타입이 앞의 프로토타입을 가리키는 것을 의미하는 용어로 **객체와 객체를 연결하는 체인의 역할**을 하는 것을 의미한다.

- 위의 예시에서 prototype chain의 활용
1. 객체 o에서 ultraProp를 찾는다.
2. 없다면 Sub.prototype.ultraProp를 찾는다.
3. 없다면 Super.prototype.ultraProp를 찾는다.
4. 없다면 Ultra.prototype.ultraProp를 찾는다.

# 참조

- [자바스크립트 자료 시각화](http://pythontutor.com/visualize.html#mode=display)