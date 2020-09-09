---
layout: post
title: 웹스크래핑13. Rendering
category: python
tags: [python, webscraping]
comments: python
---

# Rendering

### Rendering?

- router에서 직업과 관련되어서 저장된 db를 보내준다.

- db를 받을 템플릿을 작성한다.

- 각각의 job마다 html로 렌더링하기. for in 구문을 쓸 수 있다.

- flask에서 for in을 쓰기 위해서는 {% %}안에 넣으면 파이썬 코드를 실행할 수 있다. 변수는 {{ varibale }}로 보여준다.

```html
{% for job in jobs %}
<span>{{job.title}}</span>
<span>{{job.company}}</span>
<span>{{job.location}}</span>
<span>{{job.link}}</span>
{% endfor %}
```

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