---
layout: post
title: javascript-09 arguments
category: javascript
tags: [javascript, arguments]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6548)강의를 요약, 정리한 글입니다.  

# argument

### arguments의 정의

- argument 자바스크립트와 사용자간에 약속한 특수한 변수 명이다. arguments 객체는 함수에 전달된 **인수**에 해당하는 **Array 형태의 객체**이다.

### arguments의 필요성

- 함수에 전달된 인수의 개수를 파악할 때 쓰인다. 이것을 **반복문과 함께 쓰면** 매개변수 숫자에 따른 결과값을 만들어낼 수 있다. 아래는 예제코드이다.

```javascript
function sum(){
    var i, _sum = 0;    
    for(i = 0; i < arguments.length; i++){
        document.write(i+' : '+arguments[i]+'<br />');
        _sum += arguments[i];
    }   
    return _sum;
}
document.write('result : ' + sum(1,2,3,4));
```

### arguments의 활용

- 매개변수와 관련된 두가지 수가 있다. 하나는 함수.length, 다른 하나는 arguments.length이다.

- arguments.length는 함수로 전달된 실제 인자의 수를 의미하고, 함수.length는 함수에 정의된 인자의 수를 의미한다. 아래의 코드를 보자.

```javascript
function zero(){
    console.log(
        'zero.length', zero.length,
        'arguments', arguments.length
    );
}
function one(arg1){
    console.log(
        'one.length', one.length,
        'arguments', arguments.length
    );
}
function two(arg1, arg2){
    console.log(
        'two.length', two.length,
        'arguments', arguments.length
    );
}
zero(); // zero.length 0 arguments 0 
one('val1', 'val2');  // one.length 1 arguments 2 
two('val1');  // two.length 2 arguments 1
```

