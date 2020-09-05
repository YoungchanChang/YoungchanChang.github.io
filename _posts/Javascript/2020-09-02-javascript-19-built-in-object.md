---
layout: post
title: javascript-19 표준 내장 객체
category: javascript
tags: [javascript, prototype]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6475)강의를 요약, 정리한 글입니다.  


# 표준 내장 객체

### 표준 내장 객체(Standard Built-in Obejct)란?

- 자바스크립트가 공식적으로(Standard) 탑재되어(Build-in) 있는 객체(Object)들을 의미

### 표준 내장 객체를 쓰는 이유

- 표준 내장 객체는 프로그래밍을 하는데 **기본적으로 필요한 도구**들이기 때문에 중요하다. 내장객체를 이해하는 것은 프로그래밍의 기본이다.

### 표준 내장 객체의 활용

- 표준 내장객체는 js나 호스트 환경이 개발자에게 제공하는 **미리 만들어진 객체**인 반면, 표준 내장객체를 **이용하여 만든 객체는 사용자 정의 객체**라고 한다.


- 표준 내장 객체를 이용해서 메소드 만들기

```javascript
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
function getRandomValueFromArray(haystack){
    var index = Math.floor(haystack.length*Math.random());
    return haystack[index]; 
}
console.log(getRandomValueFromArray(arr));
```

<center>
<figure>
<img src="https://imgur.com/KLsfoOV.png" alt="views">
<figcaption>새로운 객체를 가리키지 않고 내부 메소드를 가리키게 된다.</figcaption>
</figure>
</center>

- 표준 내장 객체 안에 prototype을 이용해서 메소드 만들기

- 표준 내장 객체 안에 메소드를 추가했을 때 보는 사람 입장에서 해당 메소드가 어떤 내장객체와 관련있는지 알 수 있기 때문에 가독성이 높아진다는 장점이 있다.

- 공통으로 사용하는 로직이 있을 경우 내장객체에 메소드를 추가할 수 있다.

```javascript
Array.prototype.rand = function(){
    var index = Math.floor(this.length*Math.random());
    return this[index];
}
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
console.log(arr.rand());
```

<center>
<figure>
<img src="https://imgur.com/6GfrbLW.png" alt="views">
<figcaption>새로운 객체를 가리키지 않고 내부 메소드를 가리키게 된다.</figcaption>
</figure>
</center>

# 참조

- [자바스크립트 자료 시각화](http://pythontutor.com/visualize.html#mode=display)