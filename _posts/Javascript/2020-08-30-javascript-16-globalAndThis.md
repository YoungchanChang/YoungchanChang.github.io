---
layout: post
title: javascript-16 globalAndThis
category: javascript
tags: [javascript, globalAndThis]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6577)강의를 요약, 정리한 글입니다.  

# 전역객체

### 전역객체란?

- 전역객체(Global object)는 특수한 객체다. 모든 객체는 이 전역객체의 프로퍼티다.

- 아래 예제에서 window.func()로 윈도우 객체의 func()메소드를 호출할 수 있지만, 다만 편의를 위해서 윈도우의 전역객체를 생략해도 실제로 window를 붙인 것과 같이 행동한다. 그래서 func()만드로 func()메소드를 호출할 수 있다.

- 모든 함수는 전역 함수, 전역 변수라도 **윈도우 전역 객체**의 프로퍼티이다.

```javascript
function func(){
    alert('Hello?');    
}
func();
window.func();
```
- Node.js의 경우 window대신 **global전역 객체**가 존재한다.


# this

### this란?

- this는 함수 내에서 함수 호출 맥락(context)를 의미한다. **함수를 어떻게 호출하느냐**에 따라서 this가 가리키는 대상이 달라진다는 뜻이다.


### 함수 메소드 소속의 this

- 아래 예제에서 this는 전역객체인 window를 카리킨다. 모든 함수는 윈도우 전역 객체의 프로퍼티이기 때문이다.

```javascript
function func(){
    if(window === this){
        document.write("window === this");
    }
}
func(); 
```

### 객체 소속의 this

- 객체의 소속인 메소드의 this는 그 객체를 가르킨다.

```javascript
var o = {
    func : function(){
        if(o === this){
            document.write("o === this");
        }
    }
}
o.func();  
```

### 생성자를 호출했을 때의 this

- **함수를 호출**했을 때와 new를 이용해서 **생성자를 호출**했을 때의 차이

```javascript
var funcThis = null; 
 
function Func(){
    funcThis = this;
}
// 함수를 호출
var o1 = Func();
if(funcThis === window){
    document.write('window <br />');
}
// 생성자를 호출
var o2 = new Func();
if(funcThis === o2){
    document.write('o2 <br />');
}
```

### 생성자가 선언되지 않은 상태에서 변수 할당

- 생성자는 빈 객체를 만든다. 그리고 이 객체내에서 **this는 만들어진 객체를 가르킨다**. 이것은 매우 중요한 사실이다. 생성자가 실행되기 전까지는 객체는 변수에도 할당될 수 없기 때문에 this가 아니면 객체에 대한 어떠한 작업을 할 수 없기 때문이다. 

```javascript
function Func(){
    document.write(o);
}
var o = new Func(); //undefined
```

### this값을 제어하는 방법

- **apply메소드를 이용하면 this값을 제어**할 수 있다.

```javascript
var o = {}
var p = {}
function func(){
    switch(this){
        case o:
            document.write('o<br />');
            break;
        case p:
            document.write('p<br />');
            break;
        case window:
            document.write('window<br />');
            break;          
    }
}
func();
func.apply(o);  // o객체에 func()메소드가 소속되게 된다. this는 o객체를 가리킴
func.apply(p);  // p객체에 func()메소드가 소속되게 된다. this는 p객체를 가리킴
```