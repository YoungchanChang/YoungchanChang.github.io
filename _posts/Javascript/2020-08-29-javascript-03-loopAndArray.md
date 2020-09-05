---
layout: post
title: javascript-03 반복문, 배열
category: javascript
tags: [javascript, loop, Array]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

# 반복문, 배열의 관계

- 특정 조건이 맞을 때까지 작업을 계속하게 할 수 있다 - 반복문
- 일반적으로 같은 종류의 데이터들이 순차적으로 저장되어 있는 구조를 배열이라고 한다.
- 반복문은 배열과 매우 밀접한데, 같은 종류의 데이터들을 반복적으로 처리할 때 주로 반복문으로 처리하기 때문이다.

# 반복문

### 반복문의 정의

- 반복문은 컴퓨터가 동작하는 방법을 **조건에 따라 반복**하는 역할을 한다.

### 반복문을 쓰는 이유

- 반복문을 쓰는 이유는 인간이 하기 귀찮은 반복되는 일을 컴퓨터에게 시킬 수 있기 때문이다.

### 반복문을 쓰는 방법

- 반복문은 while문, for문 2가지로 쓸 수 있다. 상황에 따라서 맞게 쓰면 된다.

- **while문**

```javascript
1초기화
// 종료조건으로 i의 값이 10보다 작다면 true, 같거나 크다면 false가 된다.
while (2.반복조건){
    
    3반복해서 실행될 코드

    4.반복해서 실행할 코드
}

```
- **for문**

```javascript
for(1초기화; 2반복조건; 4반복이 될 때마다 실행되는 코드){
    3반복해서 실행될 코드
}
```
- 반복문의 순서이다. 1.초기화를 한다. 2. 반복조건이 실행된다. 3. 참이면 중괄호의 내용이 실행된다. 4. 반복이 될 때마다 실행되는 코드가 실행된다. 
- 다시 2번으로 가서 3, 4로 반복한다.

### 반드시 알아야 할 사항

- **Break**
- 반복작업을 중간에 중단시키고 싶다면 break를 사용하면 된다. (**나가기**)

```javascript
for(var i = 0; i < 10; i++){
    if(i === 5) {
        break;
    }
    document.write('coding everybody'+i+'<br />');
}
```
- **continue**
- 실행을 즉시 중단 하면서 반복은 지속되게 하려면 continue를 쓴다. (**특정 조건만 건너뛴다.**)

```javascript
for(var i = 0; i < 10; i++){
    if(i === 5) {
        continue;
    }
    document.write('coding everybody'+i+'<br />');
}
```
# 배열

### 배열의 정의

- 배열은 **번호와 번호에 대응 하는 데이터**들로 이루어진 구조로 일반적으로 **같은 종류의 데이터들이 순차적**으로 저장


### 배열을 쓰는 이유

- 변수가 하나의 데이터를 저장하기 위한 것이라면 배열은 여러 개의 데이터를 하나의 변수에 저장하기 위한 것이다.
- 특히 반복문과 같이 쓰면 여러 개의 데이터를 빠르게 처리할 수 있다.

### 배열을 쓰는 방법

- 배열의 생성,읽기,수정,삭제

- 배열을 생성할 때는 [] 대괄호를 통해 생성한다.
- 배열을 읽을 때는 배열[index]로 읽는다.
- 배열은 대입연산자를 통해서 수정 가능
- 배열의 특정 index를 삭제할 때는 배열 내부에 splice()함수로 수정이 가능하다.

```javascript
//배열의 생성
var memberArray = ['egoing', 'graphittie', 'leezhce'];
//배열의 읽기
console.log("memberArray[2]", memberArray[2]);
//배열의 수정
memberArray[0] = 'leezche';
//배열의 삭제
memberArray.splice(index, 1)
```


### 기타 알아야 할 사항

- 배열의 크기를 알아내기

- 반복문을 쓸 때 조건값으로 배열의 크기가 쓰인다.

```javascript
var arr = [1, 2, 3, 4, 5];
for(var i = 0; i < arr.length; i++){ }
```

- 배열에 값을 추가하기

- 데이터를 추가할 때 쓰인다. 예를 들어서 회원가입을 한 경우 회원 목록에 추가할 때 쓸 수 있다.

```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li.push('f');
var list = li.concat(['f', 'g']);
```

- 여기서 push()는 **원본 배열**에 새로운 값을 추가하는 방식이고, concat()은 새로운 값을 추가한 **새로운 배열**을 만드는 방식이다.

- 두 방식이 같아보이지만 React에서 ShouldComponentUpdate()라는 메소드를 쓸 때는 **새로운 배열로 값을 처리**해야 되서 concat()을 주로 쓴다.