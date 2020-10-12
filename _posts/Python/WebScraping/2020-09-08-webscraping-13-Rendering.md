---
layout: post
title: 웹스크래핑13. Rendering
category: webscraping
tags: [python, webscraping]
comments: python
---

# Rendering

### Rendering?

- router에서 직업과 관련되어서 저장된 db를 보내준다.

- db를 받을 템플릿을 작성한다.

- 각각의 job마다 html로 렌더링하기. for in 구문을 쓸 수 있다.

- flask에서 for in을 쓰기 위해서는 % %안에 넣으면 파이썬 코드를 실행할 수 있다. 변수는 {{ varibale }}로 보여준다.

```python
# {% for job in jobs %}
<span>{{job.title}}</span>
<span>{{job.company}}</span>
<span>{{job.location}}</span>
<span>{{job.link}}</span>
# {% endfor %}
```
<!-- 반드시 jobs가 서버에서 넘어와야한다.
팡썬코드에서 html을 친다면 {%%}를 넣어야한다. 파이썬 코드 실행 {{}} 변수 넣기 -->

- cs코드는 grid덕분에 예쁘게 보인다.

### 참고로 알아야 할 사항

- grid template

```html
<style>
    section{
        display:grid;
        gap:20px;
        grid-template-columns : repeat(4, 1fr);
    }
</style>
```
