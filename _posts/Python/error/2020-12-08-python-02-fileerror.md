---
layout: post
title: 파이썬 fuzzyuzzy에러
category: python
tags: [python, program]
comments: true
---

> [참고](http://blog.naver.com/PostView.nhn?blogId=chandong83&logNo=220979166817&parentCategoryNo=&categoryNo=44&viewDate=&isShowPopularPosts=true&from=search)

# 에러 코드

- UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc0 in position 0: invalid start byte

- 뜻 : 유니코드디코드 에러. utf-8 코덱은 0xc0을 해석할 수 없다.

- 실제로 �̸�@����라고 나와있다.

# 에러 발생 상황

- `process.extractOne(args1, args2, scorer=fuzz.partial_ratio)`메소드를 수행했을 때 에러

# 에러 발생 원인

- args1은 문자열, args2는 배열을 넣었어야 하는데,  parse_"string"이 아니라 배열을 넣었었다.

- 문자열 대신에 nan을 넣은 경우 위와 같은 현상 발생

# 로우레벨로 읽어서 출력을 해보기

```python
# -*- coding: utf-8 -*-
path = 'd:/test.txt'
with open(path, 'rb') as f:
    buf  = f.read()
    print(buf)
```

- 실제로 파일을 읽어보면 "\xc0\"와 같은 문제가 있다.

# 해결방법

- get_data()로 썼다.

> [참조](https://www.python2.net/questions-16237.htm)
