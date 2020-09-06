---
layout: post
title: 웹스크래핑05. 웹 페이지의 페이지 리스트 정보 가져오기
category: python
tags: [python, webscraping]
comments: python
---

### 웹 페이지의 페이지 리스트 정보 가져오기

    - 리스트의 숫자만큼 반복해서 내용을 가져올 예정
    
### 과제 진행 순서

1] find()메소드로 pagination 부분에 해당하는 태그 내용만 추출.

2) find_all()메소드로 **a태그의 내용만 추출**. 리스트값 반환

3] for in 구문을 활용하여 리스트 중에서 번호에 해당하는 부분만 추출. 마지막은 next부분으로 숫자가 아님으로 출력하지 않는다.

4] 리스트 안에서 최대 값 찾기

5] 요청 파라미터 만들기

### 과제 세부 진행

1] find()메소드로 pagination 부분에 해당하는 태그 내용만 추출.

```python
import requests
from bs4 import BeautifulSoup

indeed_url = "https://kr.indeed.com/jobs?q=python"
indeed_result = requests.get(indeed_url)

indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')
indeed_extract = indeed_soup.find('div', {'class' : 'pagination'}) # div태그안의 pagination 클래스 태그를 추출한다. find()메소드로 리턴값은 한 줄의 태그이다!

print(indeed_extract)
```

2] find_all()메소드로 **a태그의 내용만 추출**. 리스트값 반환


```python
indeed_pages_a_tag = indeed_pages.find_all('a') # 내용중에 a태그의 내용만 리스트로 반환

print(indeed_pages_a_tag)
```

3] for in 구문을 활용하여 리스트 중에서 페이지에 해당하는 부분만 추출. 마지막은 next부분으로 숫자가 아님으로 출력하지 않는다.

```python
page_collect = []
for page_num in indeed_pages_a_tag: # 리스트안의 내용을 반복해서 출력
    # print(page_num.find('span'))
    page_collect.append(page_num.find('span').string)

page_collect = page_collect[0:-1]
print(page_collect)
```

4] 리스트 안에서 최대 값 찾기

- string 배열에서 최대값 찾기

```python
page_collect = []
for page_num in indeed_pages_a_tag[:-1]: # 리스트안의 내용을 반복해서 출력
    page_collect.append(page_num.find('span').string)

max_page = int(max(page_collect)) # 리스트 안에서 최대 숫자 찾기

for n in range(max_page):
    print(requests.get(f"{indeed_url}&start={n*LIMIT}"))
```

- int로 변환한 뒤에 최대값 찾기

```python
page_collect = []
for page_num in indeed_pages_a_tag[:-1]: # 리스트안의 내용을 반복해서 출력
    page_collect.append(int(page_num.find('span').string))

max_page = page_collect[-1] # 리스트 안에서 최대 값 찾기

for n in range(max_page):
    print(requests.get(f"{indeed_url}&start={n*LIMIT}"))
```

5] 요청 파라미터 만들기

```python
for n in range(max_page):
    print(requests.get(f"{indeed_url}&start={n*LIMIT}"))
```

### HTTP 요청 메서드 중 GET방식이란

- HTTP메서드중 GET은 URL의 **query string을 통해 데이터를 요청**한다.

- 서버에 한 페이지에 10개씩 데이터를 요청하는 방식은 아래와 같다. 여기서 "&start=10"부분을 규칙적으로 만들면 된다.

```
https://kr.indeed.com/jobs?q=python&start=10

https://kr.indeed.com/jobs?q=python&start=20

https://kr.indeed.com/jobs?q=python&start=30
```


# 참고

[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)
[import from](http://cloudrain21.com/python-difference-between-import-from-import)