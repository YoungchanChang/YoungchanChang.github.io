---
layout: post
title: 파이썬 string
category: python
tags: [python]
comments: true
---

- 파이썬의 변수와 데이터타입에 대해서 다룹니다. Numeric, String, Boolean, List, 튜플, 딕셔너리에 대해 간략히 소개합니다.

# String

### 문자열이란?

- 문자를 쭉 나열한 것
- 큰 따옴표나 작은 따옴표로 묶으면 문자열이 된다.
- 값을 변경할 수 없고, 순서를 변경할 수 없다.

```python
my_str = "김씨가족"
print(my_str) # 변수 값 출력
type(my_str) # 변수 데이터형 출력
```

- """큰 따옴표 세개로로도 문자열을 만들 수 있다.
- 여러 줄을 한 변수에 저장할 수 있다.

```python
>>> my_str = """제스퍼
토미
메타
"""
>>> print(my_str) # 변수 값 출력
```

# 문자열 Formatting

- 문자열에 숫자나 문자열을 대입하는 것

- ex> %d %f %s

- %s는 문자열을 대입할 때 쓰인다.
- 좀 더 자유롭게 표현하고 문자열에 대입해서 쓸 때 사용한다. C스타일이라고 한다.
```python
>>> my_str = 'My name is %s' % 'Young Choi' # 영최 문자열이 %s로 대입이 된다.
>> my_str

>>> '%d %d' % (1, 2) # 정수형 숫자를 대입할 때 %d를 쓴다.
```

# format()연산자
- 파이썬에서는 %보다 forat()연산자를 많이 사용한다.
- 중괄호를 이용한다.
- 결과는 같지만 format()이 파이썬스럽다.
- 문자열을 자유롭게 쓰기 위한 방법이다.
- {}안에 숫자를 지정해서 format의 파라미터 순서를 정할 수 있다.
```python
// %와 format()비교
>>> 'My name is %s' % '테스터'
>>> 'My name is {}'.format('테스터')

// format()예시
>>> '{} x {} = {}'.format(2, 3, 2*3)

// format()예시2
>>> '{1} x {0} = {2}'.format(2, 3, 2*3)
```
- f""로 .format()을 대신할 수 있다.
[python f-string](https://www.python-course.eu/python3_formatted_output.php)

# 인덱싱

- Index는 주소, 위치를 의미한다.
- space도 한 문자로 처리한다.
- 음수로도 처리할 수 있다. 제일 마지막이 -1, 그 다음이 2 순서로 진행된다.

```python
>>> my_name = "장영찬의 코딩"
# 0번 index - 장, 1번 index 영

>>> my_name[3] #인덱스 값 확인
```

# Slicing

- 문자열을 자를 때 쓴다. 대괄호 안에 자르려는 문자 인덱싱 번호를 넣는다.
- slice(start, stop)에서 start, stop는 인덱스 번호를 가리키고 **사이 값**을 가져올 수 있다.
- ex) [1:4] 시작값, 멈추는 값
- 앞에 숫자가 없으면 처음부터 그 숫자 전까지, 뒤에 숫자가 없으면 앞에 숫자부터 끝까지 진행한다.
- ex) [:3] [2:]

```python
my_name[5:7]
```

# 메서드
- 스트링만이 사용할 수 있는 함수를 스트링 메서드라고 한다.
- `string.split()` : 문자를 공백 단위로 리스트에 나뉘어서 저장되게 된다.

- 예시
```python
>>> my_name.split()

>>> fruit_str = '거봉 수박 포도 복숭아 망고 딸기 배 참외 찹쌀떡'
>>> fruists = fruit_str.split()
```

# Docsting
- 큰 따옴표를 이용해서 주석처리를 할 수 있다. 
- 큰따옴표 세개로 문자열을 만들 때 이름을 붙이지 않으면 된다.
- 보통 함수 설명을 할 때 쓰인다.
```python
>>> #이것이 주석입니다.
>>> """이것도 주석입니다."""
```

# end, 이스케이프 코드
- end
- 출력의 두번째 파라미터로 end를 쓰면 출력의 끝을 지정할 수 있다.

```python
print('집단지성')
print('집단지성', end='')
print('집단지성', end='/')
```

- 문자열 안에 이스케이프 코드를 쓰면 특별한 행동을 하게 된다.
- '\n'은 엔터의 역할을 한다. \t는 탭의 역할을 한다. 문자열 안에 이스케이프코드를 쓰면 된다.

```python
print('미운코딩새끼의\n집단지성들')
print('미운코딩새끼의\t집단지성들')
```


### 추가로 알아두면 좋을 사항

- f-string

# 참조
- [슬라이스 파이썬 공식문서](https://docs.python.org/ko/3/library/functions.html?highlight=slice#slice)
- [파이썬 온라인](repl.it)
- 왜 쓰는지, 언제쓰는지에 대한 설명이 부족했다. 실용적인 예시가 없어서 아쉬웠다.
