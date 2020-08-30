---
layout: post
title: javascript-06 유효범위
category: javascript
tags: [javascript, API]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

- 모듈, API, 레퍼런스, 튜토리얼, 정규표현식의 개념에 대해 작성함

# 유효범위

### 유효범위란?

- 유효범위(Scope)는 **변수의 수명**을 의미한다. 자바스크립트에서 변수는 유효 범위에 따라 지역 변수(local variable)와 전역 변수(global variable)로 구분된다.

### 유효범위를 쓰는 이유

- 유효범위는 변수를 전역변수와 지역변수를 나눠서 좀 더 편리하게 관리할 수 있다. 변수를 전역변수처럼 **프로그램 전체에서 접근**하게 된다면 복잡한 변수들로 인해 예기치 못한 문제가 발생하게 된다. 그런데 지역변수를 사용하면 **해당 변수가 영향을 미치는 유효 범위를 제한**할 수 있기 때문에 전역변수를 쓸 때의 문제가 줄어든다.

### 유효범위를 쓰는 방법

- 함수 밖에서 변수를 선언하면 그 변수는 전역변수가 되고, 함수 안에서 변수를 선언하면 지역변수가 된다.

```javascript
var globalNum = 20;
function localNum() {
    var num = 10; // 지역 변수 num에 숫자 10을 대입함.
    document.write("함수 내부에서 변수 num의 타입은 " + typeof num + "입니다.<br>"); // number
}

localNum();       // 함수 localNum()을 호출함.
document.write("함수의 호출이 끝난 뒤 변수 num의 타입은 " + typeof num + "입니다."); // undefined
document.write("함수의 호출이 끝난 뒤 변수 num의 타입은 " + globalNum + "입니다."); 
```

- **자바스크립트는 함수에 대한 유효범위만을 제공**한다. 많은 언어들이 블록(대체로 {,})에 대한 유효범위를 제공하는 것과 다른 점이다. 아래 예제의 결과는 coding everybody이다. 반면, 자바의 코드가 실행되지 않는다.

```javascript
for(var i = 0; i < 1; i++){
    var name = 'coding everybody';
}
alert(name);
```
```java
for(int i = 0; i < 10; i++){
    String name = "egoing";
}
System.out.println(name);
```

### 반드시 알아야 할 사항

- **전역변수는 사용하지 않는 것**이 좋다. 여러가지 이유로 그 값이 변경되면 버그가 날 가능성이 있기 때문이다.

- 변수를 선언할 때는 꼭 var을 붙이는 것을 습관화해야 한다. 전역변수를 사용해야 하는 경우라면 그것을 사용하는 이유를 명확히 알고 있을 때 사용하도록 하자

- 불가피하게 전역변수를 사용해야 하는 경우는 **전역변수용 객체를 만들고** 객체의 속성으로 변수를 관리하는 방법을 사용한다.

```javascript
MYAPP = {}
MYAPP.calculator = {
    'left' : null,
    'right' : null
}
MYAPP.coordinate = {
    'left' : null,
    'right' : null
}
 
MYAPP.calculator.left = 10;
MYAPP.calculator.right = 20;

function sum(){
    return MYAPP.calculator.left + MYAPP.calculator.right;
}

document.write(sum());
```

### 추가로 알아야 할 점

- for문에서 변수 i를 선언하면 중괄호 안에서만 유효한 지역변수가 된다.

- 지역변수의 유효범위는 함수 안이고, 전역변수의 유효범위는 에플리케이션 전역인데, 같은 이름의 지역변수와 전역변수가 동시에 정의되어 있다면 지역변수가 우선한다

- 자바스크립트에서 **객체나 함수는 모두 변수(variable)**이다. 

- 자바스크립트는 함수가 호출될 때가 아닌 **선언된 시점**에서의 유효범위를 갖는다. 이러한 유효범위의 방식을 정적 유효범위(static scoping), 혹은 렉시컬(lexical scoping)이라고 한다. 아래 예제의 경우 b()함수는 선언된 시점에서 i의 지역변수가 없으므로 전역변수를 쓰게 된다.

```javascript
var i = 5;
 
function a(){
    var i = 10;
    b();
}
 
function b(){
    document.write(i);
}
 
a();
```