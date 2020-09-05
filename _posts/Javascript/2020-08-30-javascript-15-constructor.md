---
layout: post
title: javascript-15 constructor
category: javascript
tags: [javascript, constructor]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6570)강의를 요약, 정리한 글입니다.  

# 객체

### 생성자란?

- 생성자(constructor)는 **객체를 만드는 역할을 하는 함수**다. 자바스크립트에서 함수는 재사용 가능한 로직의 묶음이 아니라 **객체를 만드는 창조자**라고 할 수 있다.

### 생성자를 쓰는 이유?

- **객체의 구조를 재활용**할 수 있는 방법이다. 코드의 재사용성이 높아진다.

### 생성자를 어떻게 쓰는가?

- 생성자 함수는 일반함수와 구분하기 위해서 첫글자를 대문자로 표시한다.

- 일반적인 객체지향 언어에서 생성자는 클래스의 소속이다. 하지만 자바스크립트에서 **객체를 만드는 주체는 함수**다.

- 따라서, 자바스크립트에서 **함수에 new를 붙이는 것을 통해서** 객체를 만들 수 있다

```javascript
function Person(name){
    this.name = name;
    this.introduce = function(){
        return 'My name is '+this.name; 
    }   
}
var p1 = new Person('egoing');
document.write(p1.introduce()+"<br />");
 
var p2 = new Person('leezche');
document.write(p2.introduce());
```

### 추가로 알아두면 좋을 사항

- javascript에서 프로퍼티는 값을 나타낸다. 프로퍼티는 이름(string)과 값(primitive, method, object reference)로 이루어진다.

- javascript에서는 함수가 객체이고 값으로 작동한다. 

- java의 프로퍼티가 변수와 유사하지만, javascript에서는 함수의 값을 담을 수 있다.


# 참조
[자바 은닉화](https://mainpower4309.tistory.com/7)
[자바스크립트 프로퍼티](https://m.blog.naver.com/magnking/220966405605)