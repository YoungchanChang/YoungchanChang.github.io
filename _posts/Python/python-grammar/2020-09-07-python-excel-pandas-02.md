---
layout: post
title: 파이썬 엑셀 판다스 활용해서 읽고 쓰기
category: python
tags: [python, 쓰기]
comments: true
---

# Pandas 필요한 열 추출하기

- loc를 이용
       - []안의 앞에는 전체를 의미하는 ':'를, 뒷자리에는 선택할 열 이름으로 구성된 list를 넣는다.
       - 모든 행(:)의 선택한 열만 보겠다는 의미

- 이중리스트 사용

```
df_sample = data.loc[:, ['성별', '신장', '체중]]
# df_sample = data[['성별', '신장', '체중]]
```

# 한 행이나 한 열씩 처리

- 한 열씩 처리 : iteritems()를 사용
       - 하나의 열씩 컬럼명과 같이 값을 더블 형태로 취득

```python
import pandas as pd

df = pd.DataFrame({'age': [24, 42], 'state': ['NY', 'CA'], 'point': [64, 92]},
                  index=['Alice', 'Bob'])

for column_name, item in df.iteritems():
    print(type(column_name))
    print(column_name)
    print('~~~~~~')

    print(type(item))
    print(item)
    print('------')

    print(item['Alice'])
    print(item[0])
    print(item.Alice)
    print('======\n')
```


- 반복처리 중 특정 컬럼의 값만 출력하고 싶은 경우
       - 컬럼명을 지적해 출력

```python
import pandas as pd

df = pd.DataFrame({'age': [24, 42], 'state': ['NY', 'CA'], 'point': [64, 92]},
                  index=['Alice', 'Bob'])

for age in df['age']:
    print(age)
# 24
# 42
```

- 한 행씩 처리 :  iterrows()와 itertuples() 메서드
       - iterrows() : 컬럼명 또는 인덱스를 지정해 해당하는 열의 값을 취득
       - itertuples() : 각각의 값에 접근해 취득


# 참고

[필요한 열 추출](https://m.blog.naver.com/PostView.nhn?blogId=rising_n_falling&logNo=221622971970&proxyReferer=https:%2F%2Fwww.google.com%2F)

[필요한 열 추출2](http://hleecaster.com/python-pandas-selecting-data/)

[한 행씩 반복해서 추출](https://ponyozzang.tistory.com/609)