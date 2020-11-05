---
layout: post
title: 파이썬 Context Manager
category: python
tags: [python, dictionary]
comments: true
---

# 컨텍스트 매니저

- 파이썬에서 아래와 같은 코드를 보았다. with as 가 쓰였는데 무슨 말인지 잘 모르겠었다. 보통 파일읽기에서 쓰였는데, 왜 이게 쓰여야되는지 몰랐다.

```python
# Using the `close()` method.
sess = tf.compat.v1.Session()
sess.run(...)
sess.close()

# Using the context manager.
with tf.compat.v1.Session() as sess:
  sess.run(...)
```

# 컨텍스트 매니저가 쓰이는 이유

- 특정 행동을 할 때 항상 일정한 런타임 환경을 만들어주기 위해 **특정 행동에의 진입과 종료를 관리**해주는 친구가 바로 context manager이다. session()을 쓰는 이유는 끝나고 닫아주기 위해서이다.

- 컨텍스트 매니저는 직접 만들 수 있다.



# 참조

[컨텍스트 매니저](https://suhwan.dev/2017/12/29/Python3-Context-Manager/)

[텐서플로우](https://www.tensorflow.org/api_docs/python/tf/compat/v1/Session)

[파일읽기쓰기에서withas](https://twpower.github.io/17-with-usage-in-python)