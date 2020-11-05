---
layout: post
title: 웹스크래핑04. html파일에서 내가 저장하려는 정보 추출하기
category: webscraping
tags: [python, webscraping]
comments: python
---

### 가져온 html파일에서 내가 **저장하고자 하는 정보**를 추출한다.

    - beautifulsoup를 활용

    - html태그 구조를 활용
    
### 과제 진행 순서

1] [BeautifulSoup 설치](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

2] BeautifulSoup를 활용해 원하는 태그의 내용 추출하기. 아래 코드에서는 a태그 안의 결과만 추출한다.

3] 태그 안에서 속성이 jobTitle인 내용 추출하기

4] find()메소드를 통해서 직업 가져오기

5] 회사 이름과 지역 이름 가져오기

6] 코드 리팩토링하기

### 과제 상세 진행

1] [BeautifulSoup 설치](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

```
$ pip install beautifulsoup4
```

2] BeautifulSoup를 활용해 원하는 태그의 내용 추출하기. 아래 코드에서는 a태그 안의 결과만 추출한다.

- find_all()메소드를 사용해서 리스트로 전부 가져온다.

```python
import requests
from bs4 import BeautifulSoup


indeed_url = "https://kr.indeed.com/jobs?q=python"
indeed_result = requests.get(indeed_url)

indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser') # html텍스트를 파싱
indeed_extract = indeed_soup.find_all('a') # a태그만 추출

print(indeed_extract)
```

3] 태그 안에서 속성이 jobTitle인 내용 추출하기

```python
indeed_job_title = indeed_soup.find_all(attrs={"data-tn-element":"jobTitle"}) # 내용중에 a태그의 내용만 리스트로 반환
```

4] find()메소드를 통해서 **직업 가져**오기

```python
# for jobs in indeed_job_title:
#     job_title.append(jobs.get_text()) # 정규식 처리가 필요함

for jobs in indeed_job_title:
    job_title.append(jobs.attrs['title'])

print(job_title)
```

5] **회사 이름과 지역 이름** 가져오기

```python
job_company = []
indeed_job_company = indeed_soup.find_all('span', {'class' : 'company'})
for jobs in indeed_job_company:
    job_company.append(jobs.string)

job_location = []
indeed_job_location = indeed_soup.find_all('span', {'class' : 'location'})
for jobs in indeed_job_location:
    job_location.append(jobs.get_text())

print(job_location)

```

6] 코드 리팩토링하기

```python
job_info = []
indeed_job_info = indeed_soup.find_all(attrs={"data-tn-component":"organicJob"})
for jobs in indeed_job_info:
    jobs_title = jobs.find(attrs={"data-tn-element":"jobTitle"}).attrs['title']
    #print(jobs.find(attrs={"data-tn-element":"jobTitle"})['title'] + "\n") 위 코드와 동일한 의미
    jobs_company = jobs.find('span', {'class' : 'company'}).get_text().strip('\n')
    jobs_location = jobs.find('span', {'class' : 'location'}).get_text()
    job_info.append({"title" : jobs_title, "comapny" : jobs_company, "location" : jobs_location})

for info in job_info: # 코드 확인하기
    print(info)
```

# 전체코드

```python
import requests
from bs4 import BeautifulSoup

indeed_url = f"https://kr.indeed.com/jobs?q=python"
indeed_result = requests.get(indeed_url)

indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')

job_info = []
indeed_job_info = indeed_soup.find_all(attrs={"data-tn-component":"organicJob"}) # 내용중에 a태그의 내용만 리스트로 반환
for jobs in indeed_job_info:
    jobs_title = jobs.find(attrs={"data-tn-element":"jobTitle"}).attrs['title']
    jobs_company = jobs.find('span', {'class' : 'company'}).get_text().strip('\n')
    jobs_location = jobs.find('span', {'class' : 'location'}).get_text()
    job_info.append({"title" : jobs_title, "comapny" : jobs_company, "location" : jobs_location})

for info in job_info:
    print(info)
```

### 추가로 알아야 할 사항 - find_all()과 find()메소드 설명

- [find_all()](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#calling-a-tag-is-like-calling-find-all)
    - 태그 내용을 추출하고자 하면 find_all()메소드를 쓴다.

- [find()](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find)
    - find_all()은 모든 결과를 추출한 **리스트값**을 반환하지만, find()는 **하나의 결과를 반환**한다.
    - find_all()이 결과를 못찾으면 빈 리스트를 반환하지만, find()은 None이라는 키워드를 반환한다.

```python
print(soup.find("nosuchtag"))
#[]

print(soup.find("nosuchtag"))
# None
```

### 추가로 알아야 할 사항 - 속성 값 추출하기

- 원하는 리스트나 태그나 내용을 가져오기

- 특정 속성값을 갖은 태그 불러오는 방법
1. find_all(attrs={"data-tn-element":"jobTitle"})에 attr속성값 건네주기
2. indeed_soup.find('div', {'class' : 'pagination'})

- 속성 정확히 지정하고 불러오는 방법

1. jobs.attrs['title'] 속성 안에 있는 값 가져오기
2. jobs.find(attrs={"data-tn-element":"jobTitle"})['title'] 체이닝 방식으로 속성을 가져올 수 있다.
3. jobs.get_text()으로 내용 가져오기
4. jobs.string으로 내용 가져올 수 있다.

- 특정 문자열 지우는 방법
1. strip('지울 문자열')을 활용

# 참고

[속성 값 추출](https://seogwipo.tistory.com/entry/2-BeautifulSoup-%EC%97%AC%EB%9F%AC-%EA%B0%9C%EC%9D%98-%EC%9A%94%EC%86%8C-%EC%B6%94%EC%B6%9C%ED%95%98%EA%B8%B0-findall)

[Beautifulsoup API](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#kwargs)

[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners/lectures/118)
[import from](http://cloudrain21.com/python-difference-between-import-from-import)