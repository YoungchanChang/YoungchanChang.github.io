---
layout: post
title: 웹스크래핑14. ExportRoute
category: webscraping
tags: [python, webscraping]
comments: python
---

# ExportRoute

- flask에서 /export경로를 만들고 인자가 왔을 때 처리를 한다. 인자값으로는 word를 받는다.

```python
@app.route("/export")
def export():
    try:
        word = request.args.get('word')
        if not word:
            raise Exception()
    except:
        return redirect("/")
```

### try-except 처리 :

- try안의 코드를 시행한다. 만약 특정 조건에서 에러를 발생시킨다. 그러면 except블락으로 간다.

- 예외처리의 예로 내가 다이어트를 할 때 펜케익을 때를 이야기할 수 있다. 내가 팬케익을 먹으면 안 되는 상황이라 erorr가 처리된다. except는 에러를 처리한다.

- Exception이 raise되면, except문 안의 redirect("/")가 실행된다. Exception()에러라고 생각. 에러를 일으키면 redirect블락으로 간다.

- fake_db안에 vue에 해당하는 jobs가 있다. export링크를 클릭하면 vue를 db에서 찾도록 한다.(fake_db)

- html수정. export to CSV

- raise Exception()로 예외처리를 해준다.

```python
@app.route("/export")
def export():
    try:
        word = request.args.get('word')
        if not word:
            raise Exception()
        word = word.lower()
        jobs = db.get(word)
        if not jobs:
            raise Exception()
        return f"Generate CSV for {word}"
    except:
        return redirect("/")
```


