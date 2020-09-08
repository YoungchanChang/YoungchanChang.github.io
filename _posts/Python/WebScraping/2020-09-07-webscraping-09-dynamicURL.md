---
layout: post
title: 웹스크래핑09. Dynamic URL과 템플릿
category: python
tags: [python, webscraping]
comments: python
---

# Dynamic URL

- dynamic URL은 파라미터에 따라 주소값이 달라지는 경우를 의미한다.

- 사용자의 입력값이 다이나믹 할 때 쓰인다.

- <>꺽쇠 부분에 **파라미터 값을 전달**한다. 데코레이터 함수 아래에서 **해당 인자값을 쓰지 않으면** 오류가 발생한다.

```python
@app.route("/<username>")
def potato(username):
    return f"Hello {username} how are you doing"
```

# 템플릿 처리

- 사용자에게 응답하는 값은 **return 값으로 구현**이 된다.

```python
@app.route("/")
def home():
    # 사용자에게 응답하는 값
    return "<h1>Job Search</h1><form><input placeholder='What job do you want?' required/></form>"
```

- 리턴값을 html파일로 돌려줄 수 있다.
    - render_template를 import해야한다
    - 에러가 난다면 디렉터리를 만든 다음에 파일을 시행해보자.

```python
@app.route("/")
def home():
    return render_template("potato.html")
```

### 추가로 알아야 할 사항

- 위의 예시는 Controller(입력과 처리)과 View(결과 처리)의 동작을 보여준다.


# 참고
[Dynamic URL이란](https://whatis.techtarget.com/definition/dynamic-URL)

[flask json](https://riptutorial.com/ko/flask/example/5832/http-%EC%9A%94%EC%B2%AD%EC%9C%BC%EB%A1%9C%EB%B6%80%ED%84%B0-json-%EC%88%98%EC%8B%A0%ED%95%98%EA%B8%B0)

[jsonify vs json.dumps()](https://stackoverflow.com/questions/7907596/json-dumps-vs-flask-jsonify)