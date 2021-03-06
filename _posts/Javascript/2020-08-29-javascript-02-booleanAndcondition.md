---
layout: post
title: javascript-02 비교, 조건문
category: javascript
tags: [javascript, boolean, condition]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

# 비교, 조건문, 반복문, 배열의 관계

- 값을 비교하면 참, 거짓을 판별할 수 있다. - 비교
- 참, 거짓을 판별하면 특정 조건에 따라 코드를 실행시킬지 결정할 수 있다. - 조건문
- 비교를 통해 참거짓(Boolean)을 판별할 수 있으므로 조건문을 만들 수 있는 것이다.

- 특정 조건이 맞을 때까지 작업을 계속하게 할 수 있다 - 반복문
- 일반적으로 같은 종류의 데이터들이 순차적으로 저장되어 있는 구조를 배열이라고 한다.
- 반복문은 배열과 매우 밀접한데, 같은 종류의 데이터들을 반복적으로 처리할 때 주로 반복문으로 처리하기 때문이다.

# 비교

### 비교의 정의
- 프로그래밍에서 비교란 주어진 값들이 같은지, 다른지, 큰지, 작은지를 구분하는 것을 의미한다. 이 때 비교 연산자를 사용하는데 **비교 연산자의 결과는 true나 false** 중의 하나다.

### 비교를 쓰는 이유
- 비교를 통해 참거짓(Boolean)을 판별할 수 있으므로 조건문을 만들 수 있는 것이다.

### 비교를 쓰는 방법
- `==` 동등 연산자로 좌항과 우항을 비교해서 서로 값이 같다면 true 다르다면 false가 된다.

- `===` 일치 연산자로 === 좌항과 우항이 '정확'하게 같을 때 true 다르면 false가 된다. 

### 추가로 알아야 할 사항
- ===는 서로 같은 수를 표현하고 있더라도 **데이터 형이 같은 경우에만 같다고 판단**한다.

```javascript
alert(1=='1');              //true
alert(1==='1');             //false

alert(null == undefined);       //true
alert(null === undefined);      //false

alert(true == 1);               //true
alert(true === 1);              //false

alert(true == '1');             //true
alert(true === '1');            //false

alert(0 === -0);                //true
alert(NaN === NaN);             //false
```

- null과 undefined는 값이 없다는 의미의 데이터 형

- NaN은 0/0과 같은 연산의 결과로 만들어지는 특수한 데이터 형인데 숫자가 아니라는 뜻


# 조건문의 문법

### 조건문의 정의

- 조건문은 컴퓨터가 동작하는 방법을 **조건에 따라 분기**하는 역할을 한다.

### 조건문을 쓰는 이유

- 변수의 조건값에 따라서 처리 과정이 달라야 하는 경우가 존재한다. 예를 들어 로그인의 경우, 아이디와 패스워드를 올바르게 입력했을 때와 틀리게 입력했을 때 처리 과정이 달라야 한다.

### 조건문을 쓰는 방법

- 조건문은 if로 시작한다. if 뒤의 괄호에 조건이 오고, 조건이 될 수 있는 값는 Boolean이다. Boolean의 값이 true라면 조건이 담겨진 괄호 다음의 중괄호 구문이 실행된다.

```javascript
if ( 조건 ) { 
    코드 
}
```

### 추가로 알아야할 사항
- 조건문에 사용될 수 있는 데이터 형이 꼭 불린만 되는 것은 아니다. 관습적인 이유로 0는 false 0이 아닌 값은 true로 간주된다. 아래의 예제는 2를 출력한다.

```javascript
if(0){
    alert(1)
}
if(1){
    alert(2)
}
```

- 다음은 false와 0 외에 false로 간주되는 데이터형의 리스트다. if문의 조건으로 !(부정) 연산자를 사용했기 때문에 각 조건문의 첫번째 블록이 실행되는 것은 주어진 값이 false이기 때문이다.

```javascript
if(!''){
    alert('빈 문자열')
}
if(!undefined){
    alert('undefined');
}
var a;
if(!a){
    alert('값이 할당되지 않은 변수'); 
}
if(!null){
    alert('null');
}
if(!NaN){
    alert('NaN');
}
```
- 참고로 '', undefined, var a, null, NaN 모두 `==`로 비교하면 같은 값이지만 `===`로 비교하면 다른 값이된다.


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

- 반복문을 쓸 때 조건값으로 쓰인다.

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


### 비교와 불린

- JAVA에서는 숫자를 비교할 때는 동등 연산자(==), 문자열을 비교할 때는 equals()를 사용해야한다.

- Javascript는 숫자나 문자를 비교할 때 동등 연산자(==)를 쓰며 데이터 형까지 비교할 경우 일치 연산자(===)로 사용한다.
[Javascript와 변수에서 비교연산자 참조]()

- 메소드가 전역변수를 쓰는 경우 객체 안에 메소드가 종속되게 된다. 그렇게 되면 객체를 분할해서 쓰기가 어려워지게 된다. 따라서, 가급적 메소드가 **매개변수를 통해 지역변수를 설정**할 수 있다면 그렇게 하는 것이 더 바람직하다.
