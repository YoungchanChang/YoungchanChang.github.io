---
layout: post
title: 웹스크래핑06. 리팩토링
category: python
tags: [python, webscraping]
comments: python
---

- 리팩토링한 결과

- 1.get_max_pages() : 총 몇 페이지를 반복할 것인지 정보를 가져온다.

- 2.get_job_list() : **HTML정보**를 가져온 뒤 원하는 **태그 내용**을 지정한다.

- 3.get_job() : 태그에서 정확히 원하는 **정보를 추출**해서 객체로 만든다.

- 4.총 페이지만큼 반복작업을 한다.

- 5.배열값을 RETURN한다.


```python
LIMIT = 10
indeed_url = f"https://kr.indeed.com/jobs?q=python"

# 총 페이지 수 반환
def get_max_pages():
    indeed_result = requests.get(indeed_url)
    indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')
    indeed_pages = indeed_soup.find('div', {'class' : 'pagination'}) # 페이지네이션 클래스의 내용만 추출
    indeed_pages_a_tag = indeed_pages.find_all('a') # 내용중에 a태그의 내용만 리스트로 반환

    page_collect = []
    for page_num in indeed_pages_a_tag[:-1]: # 리스트안의 내용을 반복해서 출력
        page_collect.append(page_num.find('span').string)

    max_page = int(max(page_collect)) # 리스트 안에서 최대 숫자 찾기
    return max_page

# 하나의 정보만 가져오기
def get_job(html_job):
    title = html_job.find(attrs={"data-tn-element":"jobTitle"}).attrs['title']
    company = html_job.find('span', {'class' : 'company'}).get_text().strip('\n')
    location = html_job.find('span', {'class' : 'location'}).string
    return {"title": title, "comapny": company, "location": location}

# 페이지마다 request요청하면 관련된 정보를 리스트로 반환
def get_job_list(last_page):
    job_info = []
    for n in range(last_page):  # 모든 리스트에서 데이터 가져오기
        indeed_result = requests.get(f"{indeed_url}&start={n * LIMIT}")
        indeed_soup = BeautifulSoup(indeed_result.text, 'html.parser')
        indeed_job_info = indeed_soup.find_all(attrs={"data-tn-component": "organicJob"})  # 내용중에 a태그의 내용만 리스트로 반환
        for jobs in indeed_job_info:
            job_know = get_job(jobs)
            job_info.append(job_know)
    return job_info


def get_result():
    last_page = get_max_pages()
    job_list = get_job_list(last_page)
    return job_list
```