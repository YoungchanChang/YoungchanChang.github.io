---
layout: post
title: javascript-10 apply
category: javascript
tags: [javascript, apply]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6550)강의를 요약, 정리한 글입니다.  

# apply

### apply의 정의

- 자바스크립트에서 함수는 객체이다. 아래 예시 코드에서 func객체는 Function 객체가 가지고 있는 메소드들을 상속하고 있다. apply()메소드는 이 Function객체에 내장된 메소드 중 함수를 호출하는 메소드이다.

```javascript
function func(){
}
func();
```

- apply 메소드는 두개의 인자를 가질 수 있는데, 첫번째 인자는 함수(sum)가 실행될 맥락이고, 두번째 인자는 배열이다.

### apply의 필요성

- apply는 함수를 특정 객체의 소속으로 만들어 줄 수 있다.

### apply의 활용사례

- 아래 예제코드에서 sum()은 o1객체에 소속되게 된다. 이 맥락에서 this는 해당 메소드가 소속된 객체를 의미한다.

```javascript
o1 = {val1:1, val2:2, val3:3}
o2 = {v1:10, v2:50, v3:100, v4:25}
function sum(){
    var _sum = 0;
    for(name in this){
        _sum += this[name];
    }
    return _sum;
}
alert(sum.apply(o1)) // 6
alert(sum.apply(o2)) // 185

```

- sum.apply(o1)객체는 o1 = {val1:1, val2:2, val3:3, sum:sum}와 같다. 다른 점은 sum어트리뷰트가 있느냐 없느냐의 차이이다.
