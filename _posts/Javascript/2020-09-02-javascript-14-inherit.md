---
layout: post
title: javascript-14 inherit
category: javascript
tags: [javascript, inherit]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6572)강의를 요약, 정리한 글입니다.  

# 상속

### 상속이란?

- 상속은 객체의 로직을 **그대로 물려 받는** 또 다른 객체를 만들 수 있는 기능을 의미한다.

### 상속을 쓰면 좋은 이유

-  **기존의 로직을 수정하고 변경**해서 파생된 새로운 객체를 만들 수 있게 해준다. 자신의 맥락에 맞게 부모 객체의 특정 기능은 추가하거나 제거함으로써 자신의 맥락에 맞게 **부모의 로직을 재활용**할 수 있다.

### 상속을 어떻게 구현할까?

1.부모로 사용할 객체에서 property안의 값을 주기

- Person객체 안에 **prototype라는 약속되어있는 프로퍼티**가 있고 해당 프로퍼티 안에는 어떤 객체가 있다. 그리고 **객체.이름 = 값**을 통해 객체에 값을 줄 수 있고, **객체.값 = func()** 로 함수의 값을 정의함으로써 하면 해당 객체 안에 메소드를 정의할 수 있다.

```javascript
// 생성자 함수를 통해서 객체 생성
function Person(name){
    this.name = name;
}

// 객체는 name과 introduce라는 프로퍼티의 값을 주기
Person.prototype.name=null;
Person.prototype.introduce = function(){
    return 'My name is '+this.name; 
}

var p1 = new Person('egoing');
document.write(p1.introduce()+"<br />");
```

2. 상속받을 객체에서 prototype프로퍼티 객체에 값(변수 or 함수)을 집어넣는다. 객체를 상속받고 새로운 기능 추가할 수 있따.


```javascript
function Programmer(name){
    this.name = name;
}

// Programmer객체는 Person객체를 상속받는다.
Programmer.prototype = new Person();
 
// 상속받고 새로운 기능 추가
Programmer.prototype.coding = function(){
    return "hello world";
}

var p1 = new Programmer('egoing');
document.write(p1.introduce()+"<br />");
```

- prototype의 매커니즘
1.상속받을 객체의 prototype값으로 상속할 객체를 연결한다.
2.객체가 생성될 때 **prototype이라는 속성을 생성자 함수가 갖고 있는지 확인**한다.
3.생성자 함수 안에 있는 객체와 **똑같은 객체를 만들어서 생성자의 결과로 return**해준다.
4.생성된 객체의 property값이 Progammer.prototype의 객체가 된다.

- 주의할 점은 생성자를 만들지 않고 `programmer.prototype = person.prototype`으로 연결시키면 자식 객체에서 부모 객체를 건드려서 문제가 생길 수 있다.

<center>
<figure>
<img src="https://i.imgur.com/vg4Ybuo.png" alt="views">
<figcaption>자바스크립트는 prototype프로퍼티 객체를 만든다.</figcaption>
</figure>
</center>


# 참조

- [자바스크립트 자료 시각화](http://pythontutor.com/visualize.html#mode=display)
- [javascript OOP]()