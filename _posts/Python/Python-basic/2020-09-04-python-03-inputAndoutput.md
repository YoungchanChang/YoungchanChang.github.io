---
layout: post
title: 파이썬 03 - 입력과 출력
category: python
tags: [python, input, output]
comments: true
---

# 입력과 출력

- 입력은 프로그램이 **받아들이는** 데이터

- 출력은 프로그램이 **내보내는** 데이터

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
