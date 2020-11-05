---
layout: post
title: javascript-07 정규식표현
category: javascript
tags: [javascript, API]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

- 모듈, API, 레퍼런스, 튜토리얼, 정규표현식의 개념에 대해 작성함

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

# 참조
- [생활코딩 정규식 요약본](https://opentutorials.org/course/743/6580)
- [생활코딩 정규식](https://opentutorials.org/course/909/5142)
- [정규표현식을 시각화](https://regexper.com/)
- [정규표현식 빌더](https://regexr.com/)
