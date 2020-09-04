---
layout: post
title: 파이썬 엑셀 판다스 활용해서 읽고 쓰기
category: python
tags: [python, 쓰기]
comments: true
---

# Pandas란?

- **데이터 조작 및 분석**을 위해 Python 프로그래밍 언어로 작성된 소프트웨어 라이브러리

- **숫자 테이블과 시계열을 조작**하기위한 데이터 구조와 연산을 제공

# 파이썬에서 판다스를 활용한 엑셀 읽기 쓰기

### 판다스 read_excel메소드

- xls, xlsx, xlsm, xlsb, odf, ods and odt file 확장자만 읽을 수 있다.

- 파라미터 값(args)
io :  URL스트링으로, 파일을 읽어온다.

- 정해지지 않은 파라미터값(kwargs)

index_col : index로 쓸 컬럼을 정한다.

```python
# 엑셀값으로 tmp.xlsx로 읽고, index_col로 0번째 칼럼영을 적는다.
# 아래 예시에서 만약 index_col=1이라면, Name이 인덱스 칼럼이 된다.
pd.read_excel('tmp.xlsx', index_col=0)  
       Name  Value
0   string1      1
1   string2      2
```

header : 얼만만큼의 column을 header로 출력할 것인지 정한다.

`xlsx = pd.read_excel('sample.xlsx',header=10)`



- input값 : 

```python
import pandas as pd

xlsx = pd.read_excel('sample.xlsx')

print(xlsx.head())
print()
print(xlsx.tail())
print()
print(xlsx.shape) #행, 열
```

### 액셀, CSV쓰기

```python
import pandas as pd 
xlsx = pd.read_excel('./resource/sample.xlsx') 
xlsx.to_excel('./resource/pandas_result.xlsx',index=False) # index : 첫 열에 숫자 붙여주기 
xlsx.to_csv('./resource/pandas_csv.csv',index=False)

```

# 참고
[판다스 공식 문서](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html)
[CSV 쓰기](https://woolbro.tistory.com/35)