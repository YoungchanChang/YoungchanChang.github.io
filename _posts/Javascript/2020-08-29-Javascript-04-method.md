---
layout: post
title: Javascript에서 함수, 배열, 객체
category: Javascript
tags: [Javascript, JAVA, variable]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  


# 함수

### 함수의 정의

- 함수(function)란 하나의 로직을 재실행 할 수 있도록 하는 것을 의미한다.

### 함수를 쓰는 이유

- 코드의 재사용성을 높여준다. 같은 로직을 반복해야 할 때, 함수를 쓰면 한 줄만 써도 된다.

### 함수를 쓰는 방법

- 함수를 정의(define)하는 방법과 호출(call)하는 방법

- 함수를 정의할 때는 function 뒤에 함수의 이름과 소괄호를 적는다. 소괄호에 인자라는 값이 차례로 들어오는데 이 값은 함수를 호출할 때 함수의 로직으로 전달될 변수다. 인자는 생략 할 수 있다

- 함수를 호출(call)하기 위해서는 해당 `함수이름();`으로 코드를 적는다.

```javascript
function numbering(){
    i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
}
numbering();
```


### 반드시 알아야할 사항

1.함수의 핵심은 입력과 출력이다. 입력된 값을 연산해서 출력하는 것이 함수의 기본적인 역할이다. 

- 함수를 출력할 때는 `return`키워드를 쓴다. 함수는 `return` 뒤에 따라오는 값을 **함수의 결과로 반환**시키고 **함수를 종료**시킨다.

- 함수에 값을 입력하기 위해서는 인자(argument)를 쓴다. 함수를 정의할 때 쓴 소괄호에 인자 값을 넣으면 된다. 어떤 값을 인자로 전달하느냐에 따라서 함수가 반환하는 값이나 메소드의 동작방법을 다르게 할 수 있다.

```javascript
function get_argument(arg){
    return arg;
}
```

2.자바스크립트는 함수를 변수처럼 정의할 수 있다.

```javascript
var numbering = function (){
    i = 0;
    while(i < 10){
        document.write(i);
        i += 1;
    }   
}
numbering();
```



# 객체

### 객체의 정의

- 객체는 `서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것`이다.

- 여기서 객체와 배열의 차이는 배열은 **식별자로 숫자**를 사용하는 반면, 객체는 **식별자로 문자**를 사용한다.

### 객체를 쓰는 이유

- 객체를 통해 **정리정돈**을 할 수 있다.

### 객체를 쓰는 방법

- 객체의 생성, 읽기, 수정, 삭제

- 객체는 {} 중괄호로 생성한다.
- 객체는 객체.이름 OR 객체['이름']으로 값을 읽는다.
- 객체는 대입연산자를 통해서 수정 가능
- 객체는 `delete`뒤에 원하는 객체 속성을 지정해서 값을 삭제한다.

```javascript

//객체의 생성
var memberObject = {
    manager:'egoing',
    developer:'graphittie', 
    designer:'leezhce'
}

//객체의 수정
console.log("memberObject.designer", memberObject.designer);
console.log("memberObject['designer']", memberObject['designer']);

//객체의 수정
memberObject.designer = 'leezche';

//객체의 삭제
delete memberObject.manager
```

### 반드시 알아야 할 사항

1.객체에서는 반복되는 작업을 할 때 `for ( 변수 in 객체 )`구문을 쓴다.
- for 문은 in 뒤에 따라오는 배열의 key 값을 in 앞의 변수 name에 담아서 반복문을 실행한다. 
- 주의점 : `for ( 변수 in 객체 )` 구문을 사용할 때에는 객체의 접근은 .멤버변수가 아니라 대괄호[]로 진행해야 한다.
```javascript
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
for(key in grades) {
    document.write("key : "+key+" value : "+grades[key]+"<br />");
}
```

2.객체에는 객체를 담을수도 있고, 함수도 담을 수 있다. 
```javascript
var grades = {
    'list': {'egoing': 10, 'k8805': 6, 'sorialgi': 80},
    'show' : function(){
        for(var name in this.list){
            document.write(name+':'+this.list[name]+"<br />");
        }
    }
};
grades.show();
```

### 추가로 알아야 할 사항

- 다른 언어에서는 연관배열(associative array) 또는 맵(map), 딕셔너리(Dictionary)라는 데이터 타입이 객체에 해당
