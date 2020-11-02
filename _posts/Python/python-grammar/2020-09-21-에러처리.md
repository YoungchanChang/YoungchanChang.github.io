---
layout: post
title: 웹스크래핑10. Forms and Query Arguments
category: python
tags: [python, webscraping]
comments: python
---

# try-catch를 쓰는 이유

- 에러가 발생할 것 같은 코드를 try안에 넣고 except 뒤에 발생할 수 있는 에러의 이름을 적어두면, 에러 발생시 **프로그램이 멈추지 않고 별도 처리가 가능**하다.

# 에러를 직접 일으키는 방법 - raise

- 사용자가 직접 에러를 발생시키는 기능

- try안에서 발생된 에러는 catch로 간다. 그래야 유연한 프로그래밍이 가능하기 때문이다!!!

- raise Keyword로 에러를 발생시키면 에러를 관리할 때 직관적이게 관리할 수 있다!

- 에러 처리할 때

- raise문을 쓸 수도 있다.

```python
@app.route("/index")
def index2():
    abort(404)
    print('test')


@app.errorhandler(404)
def page_not_found(error):
    return render_template('page_not_found.html'), 404

```

- 아래와 같이 처리하면 에러처리를 조금 더 전문적으로 할 수 있다. except에서 raise (Keyword)의 Keyword를 가져온 뒤

- 사용자가 직접 에러를 일으킨 뒤, 해당 예외를 처리하는 부분을 따로 만든다. 404에러처리부분 raise - excep가 짝이 된다.

- 사용자가 직접 에러를 일으키려면 if else등등에서 만들 수 있다.

```python
@app.route("/")
def home():
    app.logger.error('Home')
    try:
        raise NameError('HiThere')
        return "yes"
    except NameError:
        app.logger.error('WT?')
        raise
    except:
        return "hola"
    return "Hello! Welcome to mi casa!"

@app.errorhandler(NameError)
@app.errorhandler(404)
def page_not_found(error):
    return "N!!!!!!!!!!!!!!!!!!"
```

# 에러

- 에러코드

- [문제해결] takes 0 positional arguments but 1 was given

- (https://careerkarma.com/blog/python-missing-required-positional-argument-self/)

- 파이썬에서는 객체안의 메소드는 셀프를 쓴다.

### 예외처리!!!

- 예외처리의 좋은 점은 예외 처리를 해줄 수 있을 뿐만 아니라 메시지를 보낼 수도 있다는 점이다. 에어비엔비 MEssagPArt2


# 참고

[try-catch](https://wayhome25.github.io/python/2017/02/26/py-12-exception/)

[로그 남기기](https://www.fun-coding.org/flask_advanced-4.html)

[에러 처리](https://fenderist.tistory.com/35)

[에러 강제로 발생 공식문서](https://docs.python.org/ko/3/tutorial/errors.html)

[에러 리다이렉트](https://fenderist.tistory.com/103)

[예외처리 복수개로 하기](https://ponyozzang.tistory.com/494)