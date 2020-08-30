---
layout: post
title: javascript-07 값으로서 함수와 콜백
category: javascript
tags: [javascript, API]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/4724)강의를 요약, 정리한 글입니다.  

# 값으로서의 함수

- JavaScript에서는 **함수는 객체이고 변수(variable)**이다. 다시 말해서 **일종의 값**이다. JavaScript의 함수가 다른 언어의 함수와 다른 점은 **함수가 값이 될 수 있다**는 점이다. 

- `function a(){}`코드에서 함수 a는 **변수 a에 담겨진 값**이다.

- 아래 예제에서 func(num)은 함수이지만 하나의 변수로 전달됬다.

```javascript
function cal(func, num){
    return func(num)
}
function increase(num){
    return num+1
}
function decrease(num){
    return num-1
}
alert(cal(increase, 1));
alert(cal(decrease, 1));
```

- 아래 사진을 보면 func()함수는 스택 프레임에서 객체를 가리키는 값으로 역할하고 있다.

- 변수, 매개변수, 리턴값으로 사용할 수 있는 형태의 데이터를 일급 객체라고 한다.

<center>
<figure>
<img src="https://i.imgur.com/A6jyZKp.png" alt="views">
<figcaption>함수는 객체를 가리키는 값이다.</figcaption>
</figure>
</center>


# 콜백

###

- 함수가 수신하는 인자가 함수인 경우를 콜백이라고 한다.

- 함수 앞에 .이 있다면 객체이다. 배엵개체에는 sort()함수가 있다.

- sort()는 객체에 속해있기 때문에 함수가 아닌 메소드라고 한다.

- 자바스크립트가 갖고 있는 기본 기능이기 때문에 buil-in method라고 한다.

- 콜백메서드란?

- 예시) 글작성 -> 이메일 발송 예약(짧은 시간에 끝난다.) -> 작성 완료

- 백그라운드에서 진행하면되. TODO같다. 나중에 처리해야 된다. 비동기 처리라고 한다.

- Asynchronous Javascript and XML : 




# 참조

[자바스크립트 사전](https://opentutorials.org/course/50)