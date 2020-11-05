---
layout: post
title: 파이썬 딕셔너리 처리하기
category: python
tags: [python, dictionary]
comments: true
---

# 딕셔너리 처리의 문제상황

- db 딕셔너리에서 key값이 존재하는 경우 해당 DB를 출력하는 로직을 구성중이었다. [webscrapping 12. FasterScrapping]()을 참조

```python
db = {}
db_exist = db.get(word)
#db[word] 이 두개의 차이는 무엇이지?
```


### Key로 Value를 얻는 2가지 방식

- Key로 Value얻기

```python
>>> grade = {'pey': 10, 'julliet': 99}
>>> grade['pey']
10
>>> grade['julliet']
99
```

- Key로 Value얻기(get)

```python
>>> a = {'name':'pey', 'phone':'0119993323', 'birth': '1118'}
>>> a.get('name')
'pey'
>>> a.get('phone')
'0119993323'
```

- db[word]처럼 존재하지 않는 키(nokey)로 값을 가져오려고 할 경우 db[word]는 **Key 오류를 발생**시키고 db.get(word)는 **None을 돌려준다**는 차이가 있다.

### 추가 - 딕셔너리에 값을 추가하기

```python
>>> a = {1: 'a'}
>>> a[2] = 'b'
>>> a
{1: 'a', 2: 'b'}
```

# 참조
[딕셔너리](https://wikidocs.net/16)