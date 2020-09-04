---
layout: post
title: 파이썬 04 - 반복문과 컨테이너
category: python
tags: [python, input, output]
comments: true
---

# 반복문과 배열의 관계

- 특정 조건이 맞을 때까지 작업을 계속하게 할 수 있다 - 반복문
- 일반적으로 같은 종류의 데이터들이 순차적으로 저장되어 있는 구조를 배열이라고 한다.
- 반복문은 배열과 매우 밀접한데, 같은 종류의 데이터들을 반복적으로 처리할 때 주로 반복문으로 처리하기 때문이다.

# 입력

### 입력

- input([prompt])메소드 설명

- 이 함수가 실행되면, 터미널에는 해당 함수 괄호에 입력된 문자열(argument)를 출력하고 프로그램을 중지시킨다.  사용자가 문자열을 입력하고 엔터키를 누르면 해당 메소드를 대체하여 지정한 변수에 저장한다.

```python
>>> s = input('--> ')
--> Monty Python's Fling Circus
>> s
"Month Python's Flying Circus"

```

### 반드시 알아야 할 사항

- 값을 입력받으면 문자열(string)으로 변환시킨다. 문자열(str)과 숫자(int)가 다르다는 사실을 잊으면 안 된다.

```python
>>> in_str = input("input: ")
input : 11
>>> print(type(in_str))
<class 'str'>
>>> print("11" == 11)
False
```
- 

# 참조
[파이썬 공식문서](https://docs.python.org/3/library/functions.html)
[생활코딩 파이썬](https://opentutorials.org/course/1750/9681)
