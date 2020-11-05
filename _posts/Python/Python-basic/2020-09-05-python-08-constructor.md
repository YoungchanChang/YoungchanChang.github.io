---
layout: post
title: 파이썬 07 - 클래스
category: python
tags: [python, class]
comments: true
---

# 생성자

### 생성자란

- 생성자(constructor)는 **객체를 만드는 역할을 하는 함수**다. (constructor 구조, 틀을 만들다)

- **클래스가 인스턴스화** 될 때, 실행되도록 약속되어있는 초기화와 관련된 메소드가 생성자 메소드이다.

### 생성자를 쓰면 좋은 점

- 생성자 함수를 쓰면 **객체의 구조를 재활용**할 수 있다는 장점이 있다. 코드의 재사용성이 높아진다.

- 파이썬에서 생성자 메서드의 이름은 `"__init__"`으로 고정이다.

- 내가 생각했을 때 생성자를 통해 인스턴스 변수를 초기화해서 객체마다 다른 특성을 줄 수 있다는 점이 중요하다.

### 생성자 함수 사용하기

- 항상 **self라는 매개변수**를 먼저 만들어야 한다. 아래 예시에서 첫번째 입력값이 두번째 매개변수, 세번째 매개변수는 세번째 매개변수로 들어간다.

```python
class Cal(object):
    def __init__(self, v1, v2):
        print(v1, v2)
c1 = Cal(10, 10)
```








### 인스턴스 변수와 메소드



- 인스턴스를 생성할 때 전달된 값을 인

##### 파이썬에 메서드 추가하기

- [파이썬의 메소드와 모듈]() 참조

- v1은 지역변수이기 때문에 쓸 수 없다.

- self가 인스턴스를 의미한다. 파이썬에 메소드들은 **첫번째 매개변수**를 꼭 정의해야된다. 첫번째 매개변수는 언제나 해당 인스턴스가 된다. 해당 인스턴스를 가리키는 값이 첫번째 매개변수의 값으로 들어오게 된다.

- Cal 클래스를 실행하면 복제한 인스턴스가 만들어지면서 생성자 함수가 실행이 된다. 메소드가 실행될 때, 해당 메소드의 첫번째 매개변수로 생성한 인스턴스가 들어오도록 약속되어 있다. 두번째 매개변수가 우리가 전달한 값이 들어온다. 규칙이다.

- python은 메소드의 첫번째 인자가 instance이다. self는 변수의 이름일 뿐이기 때문에 s라고 써도 된다. 단, 관습적으로 self라고 쓴다.

```python
class Cal(object):
    def __init__(self, v1, v2):
        self.v1 = v1
        self.v2 = v2
 
    def add(self):
        return self.v1+self.v2
 
    def subtract(self):
        return self.v1-self.v2
 
 
c1 = Cal(10,10)
print(c1.add())
print(c1.subtract())
```

<center>
<figure>
<img src="https://i.imgur.com/AZoJH4K.png" alt="views">
<figcaption>self객체는 자신 instance를 가리키는 변수이다</figcaption>
</figure>
</center>

- 메소드, 인스턴스 개념은 똑같다. 표현하는 방식이 다르다.

- Instance? 전역변수와 지역변수. 인스턴스에 접근해서 v1이라는 변수를 저장할 수 있게 된다.



### 추가로 알아야 할 사항





# 참조
[파이썬 공식문서](https://docs.python.org/3/library/functions.html)
[생활코딩 파이썬](https://opentutorials.org/course/1750/9681)
