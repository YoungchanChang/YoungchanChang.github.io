---
layout: post
title: 웹스크래핑16. Forms and Query Arguments
category: webscraping
tags: [python, webscraping]
comments: python
---

# Form이란?

- **웹에서 서버에 데이터를 보내는 방식**을 의미

- get방식을 쓰면 URL의 파라미터를 통해 값이 전달된다. dynamic URL과 다른 점은 함수에 인자값이 들어있지 않다는 점이다.

- 아래 코드는 client측의 html문서이다.

```html
    <h1>Job Search</h1>
    <form action="/report" method="get">
        <input placeholder='What job do you want?' name="word" required />
        <button>Search</button>
    </form>
```

- 서버측에서 인자값을 받기 위해서는 request메서드를 이용한다.
    - `print(request.args)`를 이용하면 인자값이 dictionary형태로 값이 전달되는 것을 알 수 있다.
    - 서버측에서 html파일을 만드는 과정을 **렌더링**이라고 한다.
    - 렌더링 작업 시에 인자로 값을 넘겨주면 client측에서 인자 값을 활용할 수 있다.

```python
from flask import Flask, render_template, request

@app.route("/report")
def home():
    # print(request.args)
    word = request.args.get('word')
    return render_template("potato.html", searchingBy=word)

```


- 두번째로 고려해야 할 사항

- flask에서 json파싱

- 세번째로 고려해야 할 사항!!!!


- 입력값이 있으면 함수에서도 써야한다.



- 세번째로 고려해야 할 사항 2 !!!!!!!!!!! html 템플릿. 템플릿에서 ㄱ져와서 보여준다. VC(View, Controller)

- template을 만들 수 있다. format으로

- 템플렛에서 어떻게 가져옴? flask에서 render_template()을 쓰면 된다.


- 네번째로 고려할 사항!!!!!!!!!!!!!



- URL에 데이터를 추가한다(parameter)

- Query Argument를 아무리 추가해도 - 서버에서 처리하지 않으면 URL에 영향을 주지 않는다.

- flaks에서 request. client 서버는 request, respond구조이다!!!!!!!!!!!!!!!!!!

- request에서 인자의 이름에 대한 값을 가져오기!!!!!!!!!!!!

- request값을 렌더링해주기 위해서는 넘겨줘야한다. controller에서 view로 데이터 넘겨주기

- html에서 {{}}에다가 변수를 쓰면 된다.

- **Redirect의 개념**




- 에러처리해야됨!!!

- 서버에서 처리해야 되는 것들 : request, redirect / 어떤 서버 언어를 쓰던지
- 리다이렉트





# 참고
[Dynamic URL이란](https://whatis.techtarget.com/definition/dynamic-URL)

[렌더링이란](https://www.quora.com/What-is-meant-by-rendering-a-web-page)

[flask json](https://riptutorial.com/ko/flask/example/5832/http-%EC%9A%94%EC%B2%AD%EC%9C%BC%EB%A1%9C%EB%B6%80%ED%84%B0-json-%EC%88%98%EC%8B%A0%ED%95%98%EA%B8%B0)

[jsonify vs json.dumps()](https://stackoverflow.com/questions/7907596/json-dumps-vs-flask-jsonify)