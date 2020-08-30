---
layout: post
title: javascript OOP
category: javascript
tags: [javascript]
comments: true
---

[리액트](https://www.opentutorials.org/module/4047)

# 자바스크립트와 OOP

# 1. 객체란

- 객체는 `서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것`이다.

- 객체를 통해 **정리정돈**을 할 수 있다.

# 2. js파일 실행시켜보기

- hello.js파일을 생성한다. 파일 내용은 `console.log("hello");`로 한다.

- 터미널 창에서  `node hello.js`로 명령어를 실행시킨다.


# 3. 객체와 배열

### 배열은 반복문이랑 사용할 때 장점

- 배열 : 번호와 번호에 대응 하는 데이터들로 이루어진 구조 / 일반적으로 같은 종류의 데이터들이 순차적으로 저장

- 객체 : `서로 연관된 변수와 함수를 그룹핑하고 이름을 붙인 것`

# 배열의 생성

### 배열의 생성과 객체의 생성

- 배열은 [] 대괄호, 객체는 {} 중괄호로 생성

```javascript
var memberArray = ['egoing', 'graphittie', 'leezhce'];

var memberObject = {
    manager:'egoing',
    developer:'graphittie', 
    designer:'leezhce'
}
```

### 배열의 생성과 객체의 읽기

- 배열은 배열[index]로 접근, 객체는 객체.이름 OR 객체['이름']으로 접근

- 주의점 : `for ( 변수 in 객체 )` 구문을 사용할 때에는 객체의 접근은 .멤버변수가 아니라 대괄호[]로 진행해야 한다.

```javascript
console.log("memberArray[2]", memberArray[2]);
console.log("memberObject.designer", memberObject.designer);
console.log("memberObject['designer']", memberObject['designer']);
```


### 배열과 객체의 수정

- 대입연산자를 통해서 수정 가능

```javascript
memberArray[0] = 'leezche';
memberObject.designer = 'leezche';
```

### 삭제하기

- [javascript삭제](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) 참조

```javascript
memberArray.splice(index, 1)
delete memberObject.manager
```

# 기타 알아야 할 사항

### 배열은 반복문이랑 사용할 때 장점!!!(매우 중요)
- 여러개의 data를 반복적으로 처리할 때 거대한 작업을 할 수 있다.

```javascript
console.group('array loop');
var i = 0;
while(i < memberArray.length){
  console.log(memberArray[i])
  i = i + 1;
}
console.groupEnd('array loop');
```

- `tip! 콘솔을 console.group();`으로 묶으면 보기 좋게 시각적으로 표현해준다.

- 객체에서 사용하는 for문은 for in문이라고 한다. 객체의 값만큼 중괄호의 내용이 실행된다.

- in뒤쪽에는 객체, 앞에는 객체가 반복적으로 실행될 때마다 순번에 해당되는 원소의 **이름**이 주입될 변수가 온다.
- 객체의 각각의 속성의 이름이 와야된다. .은 안 되고 대괄호로 해야한다. memberObject[name]은 변수가 된다.
- .뒤에는 변수가 올 수 없다. / `속성의 이름이 와야한다`
- 배열에서 사용하는 대괄호로 바꿔야 한다.
- 

```javascript
console.group('object loop');
for( var name in memberObject ) {
  console.log(name, memberObject.name);
}
console.groupEnd('object loop');
```

- 반복문과 배열은 필수이다! 객체에서 반복문은 있다는 정도만 알아라!

`중요`
- 배열은 인덱스 번호로 데이터를 접근할 때 사용 / for문으로 index번호 증가시킴
- 객체는 값의 이름으로 데이터를 접근할 때 사용 / for in문으로 안에있는 이름값을 가져옴. []로 접근해야함.






```javascript

var MyMath = {

random : function(){ return Math.random(); }
}

// 객체로 안 만들 때
// 디렉터리를 배우기 싫으면 클래스로 안 만들어도 된다.
// 파일 이름 앞에 접두사를 붙인다. 디렉터리를 만들고 서로 연관된 파일을 몰아넣을 수 있다.
function random() {
  return Math.random();
}
```


# 객체 : 연관된 함수와 변수를 그루핑해서 이름을 붙인 것.

- 대명사 this. 자기 자신을 가리키는 대명사가 있다.

- [불편함]자기가 속해있는 객체가 어떤 이름을 갖게될 지 알 수 없다. 

- 왜 this? 지역변수와 전역변수가 있다. 지역은 새롭게 공간에 들어가게 된다. 그렇기 때문에 완전 새로운 공간이다.

- kim.first + kim.second로 하면 된다.

- 메소드가 자신이 속해있는 객체를 가리키는 특수한 키워드를 만들기로 약속한다. 나는, 저는같은 역할을 한다.

- this!!!

### 양산 체계를 가질 수 있다.

- constructor의 필요성. 공장의 느낌!!!

- 인자값을 넣으면 값에 따라서 객체가 초기화 된다.

- WHY NEED?
- 이전에는 중괄호를 통해서 객체를 만들 때마다 다시 정의해줘야 한다.
- 속성값 몇 개를 줌으로써 필요한 값을 빠르게 생성할 수 있게 된다.

- 같은 형태의 data이지만 그 안의 속성값이 다른 경우 속성값만 줌으로써 새롭게 찍어낼 수 있다.

- constructor을 쓰면 앞에 new를 사용함으로써 실행할 때마다 객체가 양산된다.
- constructor function의 내용을 바꾸면 갚을 2개만 받는다, 3개만 받는다가 된다.
- constructor function()에 만들어진 객체가 한번에 바뀐다.

- 객체는 템플릿이라서 똑같은 객체를 만들 수 있다.

- 객체를 찍어내는 공장을 만들기

- Date의 예시. 인자값을 넣어주면 내부적으로 해당 값을 갖고있는 객체가 생성이 된다.
- 앞에 new를 붙였을 때 객체를 만들어서 return해주고 있다.
- 인자값만 관리해주면 된다!!!
- 안에 메소드들이 있다.

- The purpose of constructor is to initialize the object of a class
- the purpose of a method is to perform a task

- 옛날에는 변수명.함수() return부분이 잘 이해가 되지 않았었다. 
- 자판기 비유


# prototype
- 왜 쓰니? 함수가 생성될 때마다 새로 만들어진다. 메모리가 낭비가 된다.

1. 프로토타입 의미
객체들이 공통으로 사용하는 속성값

2. 프로토타입 없을 때의 비효율적인 점
객체를 생성할 때 마다 같은 동작을 하는 메소드가 메모리에 계속 생긴다. => 성능 저하, 메모리 낭비

3. 프로토타입을 사용하면 좋은 점
객체들이 공통으로 사용하는 속성값을 정의해서 객체 생성마다 같은 속성값을 만드는 과정을 생략해, 성능 향상과 메모리를 효율적으로 이용할 수 있게 해준다.

- 객체가 만들어질 때 마다 실행되지 않는다. 성능의 절약. 한 번만 만들어진다.

- 중요! 저 함수를 'prototype : ' 이라면 sum()함수를 호출했을 때, 저 함수가 호출될 것을 기대하고 prototy으 출력한다.

- Sharing메소드 같다. 성능, 메모리를 절약한다.

- 특정 객체의 메소드만 다르게 동작하게 하고 싶다. 
- 프로토타입 특징 : kim객체의 sum()메소드를 호출할 때, 제일 먼저 해당 객체 자신이 sum이라는 속성을 갖고 있는지를 찾는다. 만약 lee라는 객체가 있다면 sum이라는 메소드를 정의한 적이 없어? javascript는 해당 객체 자신이 없으면 생성자인 person의 prototype의 sum의 메소드가 정의되어있는지 찾는다. 

- 생성자 함수의 prototype.함수의 이름으로 하면 cunstructor을 이용해서 객체를 생성할 때 사용하는 패턴이다.
- 생성자.prototype.함수의 이름

- 1.프로토타입의 의미 2. 생성자 함수 안에서 메소드나 속성을 직접 정의하면 어떤 비효율이 발생하는가


- 메소드를 바꾸고 싶을 때, 

- 생성자 안에서 메소드 갖는 단점. 생산성이 많이 떨어진다.

- 공통적으로 사용하는 함수를 만들고 싶다. 공통적으로 만드는 속성을 만들면 좋다.

- 생성자 함수의 원형을 정한다. 

- 이전의 결과와 똑같은 결과가 실행이 된다. 차이점 : Person Constructor생성자 함수 안에 정의하는 것이 없다.
- 한 번만 만들어지기때문에 메모리가 절약된다.

# 느낀점

- 객체와 배열의 의미를 다시 한 번 생각했다. 객체에 이름을 붙이는 자바스크립트
- 배열은 같은 데이터 형태로만 이루어져있는데 실제 테스트해보니깐 아니었다. for in은 익숙하지 않았는데 다시 해봐야겠따.
- for in에서 - .이냐 []는 처음 공부했다.
- 디렉터리로 파일 이름 구분한다는 것도 처음 알았다.
- console.group('object loop'); console.log(name, memberObject.name); console.groupEnd('object loop');
- 처음 알았다.

- 앞에 new가 붙어있으면 생성자 함수라고 부른다.