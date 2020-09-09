---
layout: post
title: 웹스크래핑11. Scrapper Integration
category: python
tags: [python, webscraping]
comments: python
---

# Scrapper Integration

- 파이썬으로 웹 크롤링한 정보와 서버를 합치는 과정

### 과정 요약

- 1.클라이언트에서 요청시 Request의 parameter을 검색 모듈에 전달한다.

- 2.파이썬에서 웹 크롤링 요청시에 해당 parameter을 이용한다. 

- 2.get_job_list() : **HTML정보**를 가져온 뒤 원하는 **태그 내용**을 지정하는 메소드
    - query값이 달라져도 태그의 모양은 같다.

### 과정 상세

- 1.클라이언트에서 요청시 Request의 parameter을 검색 모듈에 전달한다.

```python
@app.route("/report")
def report():
    word = request.args.get('word')

    if word:
        word = word.lower()
        # 요청 parameter를 검색 모듈에 전달
        jobs = get_result(word)
        print(jobs)
    else:
        return redirect("/")

    return render_template("result.html",
                           SearchingBy=word)
```

- 2.파이썬에서 웹 크롤링 요청시에 해당 parameter을 이용한다. 

```python
def get_result(word):
    indeed_url = f"https://kr.indeed.com/jobs?q={word}"
    last_page = get_max_pages(indeed_url)
    job_list = get_job_list(last_page, indeed_url)
    return job_list
```


- 영향받는 메소드

- 1.get_max_pages()(총 몇 페이지를 반복할 것인지 정보를 가져오는 메소드)

```python
# 매개변수로 indeed url을 받는다.
def get_max_pages(indeed_url):
    indeed_result = requests.get(indeed_url)
    indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')
    indeed_pages = indeed_soup.find('div', {'class' : 'pagination'}) # 페이지네이션 클래스의 내용만 추출
    indeed_pages_a_tag = indeed_pages.find_all('a') # 내용중에 a태그의 내용만 리스트로 반환

    page_collect = []
    for page_num in indeed_pages_a_tag[:-1]: # 리스트안의 내용을 반복해서 출력
        page_collect.append(page_num.find('span').string)

    max_page = int(max(page_collect)) # 리스트 안에서 최대 숫자 찾기
    return max_page
```

- 2.get_job_list() : **HTML정보**를 가져온 뒤 원하는 **태그 내용**을 지정하는 메소드
    - query값이 달라져도 태그의 모양은 같다.

```python
# 페이지마다 request요청하면 관련된 정보를 리스트로 반환
def get_job_list(last_page, indeed_url):
    job_info = []
    for n in range(last_page):  # 모든 리스트에서 데이터 가져오기
        indeed_result = requests.get(f"{indeed_url}&start={n * LIMIT}")
        indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')
        indeed_job_info = indeed_soup.find_all(attrs={"data-tn-component": "organicJob"})  # 내용중에 a태그의 내용만 리스트로 반환
        for jobs in indeed_job_info:
            job_know = get_job(jobs)
            job_info.append(job_know)
    return job_info
```