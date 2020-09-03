---
layout: post
title: javascript-16 Object
category: javascript
tags: [javascript, object]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6578)강의를 요약, 정리한 글입니다.  


# Object객체

### Object객체란?

- 객체는 데이터를 저장하는 그릇, 컨테이너이다.

- Object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체이다. 다시 말해서 아무것도 상속받지 않는 순수한 객체다

### Object객체를 왜 알아야 될까?

- Object 객체의 prototype은 모든 객체들의 prototype이 된다. 모든 객체가 사용할 수 있는 기능이다. 공통적으로 사용할 수 있는 기능이다.
- **모든 객체가 가지고 있었으면 하는 기능**이 있으면 Object의 prototype에 기능을 추가하면 된다.


- 모든 객체는 Object 객체의 프로퍼티를 가지고 있다.

### Object객체의 메소드들은 형태에 따라서 어떻게 쓸까?

- Object.keys() 객체가 갖는 여러가지 key값들을 return해준다.
ex> 배열의 경우 0, 1, 2를 리턴 index들만의 리스트를 만들어서 배열로 return한다.

- Object.toString() 객체가 갖고 있는 값이 무엇인가를 출력해준다. 메소드는 prototype.toString()인 것이 중요하다.
- 값들이나 객체 상태를 사람이 보기 편하게 출력해준다.

- prototype이 있는 것은 객체를 생성한뒤 객체.toSTring()이라고 한다.
- 없는 것은 Object.keys(arr)로 쓴다.

- new키워드로 생성한다. 생성자함수가 갖는 property는 Object.keys = function{

}

- 원형으로 생성된 객체에서는 toString()을 사용할 수 있다. 객체를 생성하고, 객체에 대한 메소드로 사용한다.

- Object객체는 모든 객체의 부모이다. Array객체를 생성할 때도, Array는 Object객체를 부모로 하는 객체가 된다.


- 원치 않는 값이 포함될 수도 있다. for in문을 동작했을 때 내가 정의한 데이터만 열거될 것이라고 기대하는 것을 저버린다.
- 정확하게 알고 있고, for in문을 쓰지 않을 경우.
