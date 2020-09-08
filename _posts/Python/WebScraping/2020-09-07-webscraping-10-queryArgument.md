---
layout: post
title: 웹스크래핑10. Forms and Query Arguments
category: python
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

# Query Arguments

- 서버측에서 클라이언트에서 요청(query)들어온 **인자값(arguments)**을 받기 위해서는 request메서드를 이용한다.
    - 아래 코드에서 `print(request.args)`를 이용하면 인자값이 dictionary형태로 값이 전달되는 것을 알 수 있다.
    - 서버측에서 html파일을 만드는 과정을 **렌더링**이라고 한다.
    - 렌더링 작업 시에 인자로 값을 넘겨주면 client측에서 인자 값을 활용할 수 있다.

- 사용자가 유효하지 않은 입력값을 입력했을 때를 처리한다.
    - **입력값이 유효한지 검증**한다. 유효하다면 편의를 위해 소문자 처리한다.
    - 입력값이 없을 때 **redirect**시킨다.

```python
from flask import Flask, render_template, request, redirect

@app.route("/report")
def home():
    # print(request.args)
    word = request.args.get('word')

    if word:
        word = word.lower()
    else:
        return redirect("/")

    return render_template("potato.html", searchingBy=word)

```

- 결과값을 나타내주는 client파일

```html
    <h1>Search Search</h1>
    <h3>
        You are looking for {{searchingBy}}
    </h3>
```



# 참고
[Dynamic URL이란](https://whatis.techtarget.com/definition/dynamic-URL)

[렌더링이란](https://www.quora.com/What-is-meant-by-rendering-a-web-page)

[flask json](https://riptutorial.com/ko/flask/example/5832/http-%EC%9A%94%EC%B2%AD%EC%9C%BC%EB%A1%9C%EB%B6%80%ED%84%B0-json-%EC%88%98%EC%8B%A0%ED%95%98%EA%B8%B0)

[jsonify vs json.dumps()](https://stackoverflow.com/questions/7907596/json-dumps-vs-flask-jsonify)