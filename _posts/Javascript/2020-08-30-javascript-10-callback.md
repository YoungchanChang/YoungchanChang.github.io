---
layout: post
title: javascript-10 값으로서 함수와 콜백
category: javascript
tags: [javascript, callback]
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

### 콜백함수란?

- 함수가 다른 함수의 인자로 전달하는 것을 콜백함수라고 한다. 다른 함수로 전달이 가능한 이유는 함수가 객체나 값으로 쓰이기 때문이다.

- 아래의 예시는 동기적 콜백이다

```javascript
function greeting(name) {
  alert('Hello ' + name);
}

function processUserInput(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
}

processUserInput(greeting);
```

### 콜백함수가 사용되는 이유

- 자바스크립트에서 콜백함수는 주로 비동기처리를 수행할 때 쓰인다.

- 비동기처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고, 순차적으로 다음 코드를 먼저 실행하는 것을 말한다.

- 비동기 처리의 예로는 클릭이나 네트워크 요청이 있다. 클릭이나 네트워크 요청 이벤트가 발생할 때 어떤 것을 할지 콜백메서드로 시스템에 미리 등록을 하면, 시스템은 그에 맞추어서 콜백메소드를 수행한다.

### 콜백함수의 사용

- 아래 예시는 특정 디렉터리에서 값을 가져왔을 때 수행하는 코드이다.

```html
<!DOCTYPE html>
<html>
<head>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
</head>
<body>
<script type="text/javascript">
    
    $.get('./datasource.json.js', function(result){
        //특정 디렉터리에서 값을 가져왔을 때 수행하는 코드
        console.log(result);
    }, 'json');
</script>
</body>
</html>
```

# 참조

[자바스크립트 사전](https://opentutorials.org/course/50)
[콜백 함수](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)