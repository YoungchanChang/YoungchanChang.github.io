---
layout: post
title: 파이썬 엑셀 읽기
category: python
tags: [python, excel, read]
comments: true
---

# 파이썬에 엑셀 읽기

### CSV 모듈 활용

- 파이썬의 csv 모듈은 csv 형식의 표 형식 데이터를 읽고 쓰는 클래스이다. 해당 모듈을 활용하면 csv파일을 읽고 쓸 수 있다.

# 엑셀 파일 읽기

### 가장 기본적인 파일 읽기

- 엑셀의 표 형식은 보통 아래와 같다

```
번호	이름	가입일시	나이
1	김정수	2017-01-19 11:30	25
2	박민구	2017-02-07 10:22	35
```

- 아래 코드를 활용하면 csv파일이 콤마로 구분되어 출력된다.

```python
import csv
with open('some.csv', newline='') as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

- 출력값

```
['번호', '이름', '가입일시', '나이']
['1', '김정수', '2017-01-19 11:30:00', '25']
```


### 방언(dialect)이 포함된 파일 읽기

- 액셀은 row와 column으로 구분되는데, 아래와 같이 한 셀 안에 식별자로 구분하는 경우가 있다.

```
번호|이름|가입일시|나이
1|김정수|2017-01-19 11:30:00|25
2|박민구|2017-02-07 10:22:00|35
```

- 이럴땐 reader()메소드에 delimiter 매개변수로 식별자 값을 전달하면 된다.

```python
with open('./resource/sample2.csv','r') as f:
    reader = csv.reader(f,delimiter = '|')
    
    for txt in reader:
        print(txt)

```

- 출력값

```
['번호', '이름', '가입일시', '나이']
['1', '김정수', '2017-01-19 11:30:00', '25']
['2', '박민구', '2017-02-07 10:22:00', '35']
```

### 딕셔너리 형태로 출력하기

- 파이썬에서 객체안에 {'key' : 'value'}로 다루는 것을 딕셔너리 형태라고 한다.

- 딕셔너리 형태는 엑셀의 가장 상단의 구분자를 key값으로 주고 각 row마다 내용 값을 value로 주는 형태가 된다.

- 딕셔너리 형태로 출력하기 위해서는 reader()메소드 대신에 DictReader()메소드르 쓴다.

```python
import csv
with open('some.csv', newline='') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)

```


- 출력값

{'번호': '1', '이름': '김정수', '가입일시': '2017-01-19 11:30:00', '나이': '25'}
{'번호': '2', '이름': '박민구', '가입일시': '2017-02-07 10:22:00', '나이': '35'}

### 딕셔너리 형태 응용하기

- 딕셔너리를 key, value로 나누어서 순차로 출력할 수 있다.

```python
with open('sample1.csv', 'r') as f:
    reader = csv.DictReader(f)
    for c in reader:
        for k, v in c.items():
            print(k, v)
        print("===================")
```

- 출력값

```
번호 1
이름 김정수
가입일시 2017-01-19 11:30:00
나이 25
===================
번호 2
이름 박민구
가입일시 2017-02-07 10:22:00
나이 35
===================
```


### 나의 생각

- csv파일은 기본적으로 행, 열의 형태를 띄고 있다.

- **배열 하나**는 행에 해당하고, **배열마다 갖고있는 값**은 열에 해당한다.

```python
{  #1열 2열 3열
    [1, 2, 3] #1행
    [4, 5, 6] #2행
    [7, 8, 9] #3행
}
```

# 참고
[파이썬 공식 문서](https://docs.python.org/ko/3/library/csv.html)
[CSV 읽기](https://woolbro.tistory.com/35)