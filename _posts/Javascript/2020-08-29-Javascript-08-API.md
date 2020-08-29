---
layout: post
title: API란
category: Javascript
tags: [Javascript, API]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

- 모듈, 

# 모듈

### 모듈의 정의

- 프로그램 내부를 **기능별 단위로 분할한 부분**으로 부품을 간단하게 떼서 **교환이 쉽도록 설계**되어 있을 때의 그 각 구성 요소를 의미한다

### 모듈을 쓰는 이유

1. 자주 사용되는 코드를 별도의 파일로 만들어서 **필요할 때마다 재활용**할 수 있다.
2. 코드를 개선하면 이를 **사용하고 있는 모든 애플리케이션의 동작이 개선**된다.
3. 코드 수정 시에 **필요한 로직을 빠르게 찾을** 수 있다.
4. **필요한 로직만을 로드**해서 메모리의 낭비를 줄일 수 있다.
5. 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 때문에 동일한 로직을 로드 할 때 시간과 네트워크 트래픽을 절약 할 수 있다.(브라우저에서만 해당)

### 모듈을 쓰는 방법

1. Html에서 모듈을 쓰는 방법
1-1) 자바스크립트 파일 확장자로 파일을 만든다.
1-2) html파일을 생성하고,html에서 head태그 안에 `<script src="js파일"></script>`코드를 넣는다.(경우에 따라서 body태그 뒤에 넣기도 한다.)
1-3) 쓰고싶은 위치에 `<script></script>`구문을 통해 구현한다.

- 예시
```javascript
function welcome(){
    return 'Hello world';
}
```
```html
<head>
    <meta charset="utf-8"/>
    <script src="greeting.js"></script>
</head>
<body>
    <script>
        alert(welcome());
    </script>
</body>
```

2. Node.js에서 모듈을 쓰는 방법
1-1) 자바스크립트 파일 확장자로 파일을 만든다.
1-2) 모듈을 만들고 싶은 확장자는 `exports`키워드를 이용한다. 구체적인 방법은 아래와 같다.

예시1) exports.이름을 통해 함수를 정의한다.
```javascript
var PI = Math.PI;
exports.area = function (r) {
return PI * r * r;
};
```

예시2) 모듈.exprots에 변수를 담은 객체를 대입한다. 해당 파일은 모듈로서 기능한다.
```javascript
const odd = '홀수';
const even = '짝수';

module.exports = { odd, even }
```

1-3) 모듈을 로드할 때는 `require`키워드를 쓴다
예시)
```javascript
var circle = require('./node.circle.js');
console.log( 'The area of a circle of radius 4 is '
           + circle.area(4));
```

# 추가로 알아야 할 사항

- 모듈이 프로그램을 구성하는 **작은 부품으로서의 로직**을 의미한다면 라이브러리는 자주 사용되는 로직을 재사용하기 편리하도록 잘 정리한 일련의 **코드들의 집합**을 의미한다



# API

### API의 개념

- API의 정의는 프로그램이 동작하는 환경을 제어하기 위해서 환경에서 제공되는 `조작 장치`이다.

- API를 쉽게 비유하면 설명서로 비유할 수 있다. 하나의 제품(어플리케이션 프로그램)을 어떻게 조작하는지(Interface) 알려준다.

### 레퍼런트와 튜토리얼

- 플랫폼에서는 일반적으로 레퍼런스와 튜토리얼을 제공한다.

- 튜토리얼은 안내서이고, 튜토리얼을 통해서 해당 환경이 어떤 기능을 제공하는가에 대한 사전에 알고 있어야 하는 것을 알아야 한다.

- 그 환경이 제공하는 명령을 찾아야 한다. refence가 사전이다.

- 튜토리얼은 문법으로 비유할 수 다면, 레퍼런스는 언어의 사전으로 비유할 수 있다.



# 정규표현식

### 정규표현식이란

- 문자열을 처리하는 방법 중의 하나로 **특정한 조건의 문자를 '검색'하거나 '치환'하는 과정**을 매우 간편하게 처리 할 수 있도록 하는 수단이다

### 정규표현식을 쓰는 이유

- 웹과 관련된, 정보와 관련된 일에서는 정규표현식이 매우 중요하다. **정보를 찾아서 처리할 때 쓰인다.**

- 나의 경우에는 **아이디값 검증, 비밀번호 검증할 때** 값의 유효성 검증을 위해 정규표현식을 썼었다.

### 정규표현식을 쓰는 방법

- 정규표현식은 컴파일(compile)과 실행(execution)으로 이루어진다.

- 컴파일(compile)
- 컴파일은 검출하고자 하는 패턴을 만드는 일이다. 이 방법은 두 가지가 있다. 아래 예쩨는 a라는 텍스트를 찾는 정규표현식을 만드는 것이다.

```javascript
var pattern = /a/
var pattern = new RegExp('a');
```

- 실행(execution)
- 1) 정규식을 이용해 문자열에서 원하는 문자를 찾아내기
- RegExp.exec()는 배열을 리턴하고 RegExp.test()는 true, false를 리턴한다.

```javascript
//배열을 리턴
console.log(pattern.exec('abcdef')); 
// true 아니면 false를 리턴
console.log(pattern.test('abcdef'));
```

- 2) 문자열의 메소드를 이용해 문자열에서 원하는 문자를 찾아내기

```javascript
// RegExp.exec()와 비슷하다.
console.log('abcdef'.match(pattern));
// 문자열에서 패턴을 검색해서 이를 변경한 후에 변경된 값을 리턴한다.
console.log('abcdef'.replace(pattern, 'A'));
```

### 추가로 알아야할 사항

- 옵션
- 정규표현식 패턴을 만들 때 옵션을 설정할 수 있다. 옵션에 따라서 검출되는 데이터가 달라진다.

```javascript
// i를 붙이면 대소문자를 구분하지 않느다.
var oi = /a/i;
console.log("Abcde".match(oi)); // ["A"];
// g를 붙이면 검색된 모든 결과를 리턴한다.
var og = /a/g;
console.log("abcdea".match(og));
```

- 캡처 
- 괄호안의 패턴은 마치 변수처럼 재사용할 수 있다. 이 때 기호 $를 사용하는데 아래 코드는 coding과 everybody의 순서를 역전시킨다.

```javascript
var pattern = /(\w+)\s(\w+)/;
var str = "coding everybody";
var result = str.replace(pattern, "$2, $1");
console.log(result);
```

- 치환 
- 아래 코드는 본문 중의 URL을 링크 html 태그로 교체한다. 

```javascript
var urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim;
var content = '생활코딩 : http://opentutorials.org/course/1 입니다. 네이버 : http://naver.com 입니다. ';
var result = content.replace(urlPattern, function(url){
    return '<a href="'+url+'">'+url+'</a>';
});
console.log(result);
```

### 추가로 드는 나의 생각

- 파이썬에서 웹 크롤링을 할 때에도 쓰일 수 있지 않을까?

### 참조
- [생활코딩 정규식 요약본](https://opentutorials.org/course/743/6580)
- [생활코딩 정규식](https://opentutorials.org/course/909/5142)
- [정규표현식을 시각화](https://regexper.com/)
- [정규표현식 빌더](https://regexr.com/)
