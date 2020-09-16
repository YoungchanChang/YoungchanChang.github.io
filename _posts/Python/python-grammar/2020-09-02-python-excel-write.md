---
layout: post
title: 파이썬 엑셀 쓰기
category: python
tags: [python, 쓰기]
comments: true
---

# 파이썬에 엑셀 쓰기

### CSV 모듈 활용

- 파이썬의 csv 모듈은 csv 형식의 표 형식 데이터를 읽고 쓰는 클래스이다. 해당 모듈을 활용하면 csv파일을 읽고 쓸 수 있다.

# 엑셀 파일 쓰기

### 가장 기본적인 파일 쓰기

- 파일을 'w' 쓰기모드로 연 뒤에 writerow()메소드를 활용해서 엑셀을 쓸 수 있다.

- writerow()는 한 줄씩을 출력하지만, writerows()는 여러 줄을 출력하게 된다.

```python
import csv
data = {[1,2,3],[4,5,6],[7,8,9],[10,11,12],[13,14,15],[16,17,18]} # 이차원 리스트
with open('sample_test.csv','w', newline='') as f:
    makewrite = csv.writer(f)

    #makewrite.writerows(data)는 아래 for문을 대체할 수 있다.
    for value in data:
        makewrite.writerow(value)
        
```

- 주의 사항은 여기서 **이차원 리스트에 값을 넣어야** 한다. 만약 객체 안에 리스트를 넣는다면 아래와 같은 오류 메시지가 뜬다.

```
data = {[1,2,3],[4,5,6],[7,8,9],[10,11,12],[13,14,15],[16,17,18]} # 이차원 리스트
TypeError: unhashable type: 'list'

```


# 참고
[파이썬 공식 문서](https://docs.python.org/ko/3/library/csv.html)

[CSV 쓰기](https://woolbro.tistory.com/36)