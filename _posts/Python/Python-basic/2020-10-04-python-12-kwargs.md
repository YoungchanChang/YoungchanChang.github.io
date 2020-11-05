---
layout: post
title: 파이썬 12 - kwargs
category: python
tags: [python, inherit]
comments: true
---

# kwargs의 필요성

- 함수 인자를 순서대로 기억하는 것보다 이름으로 기억하는 것이 편하다.

- 함수에서 값을 넘겨줄 때 보통 순서대로 값을 넘겨주게 된다.

```python
def plus(a, b):
    return a - b

result = plus(30, 1)
print(result)
```

- 인자의 위치에 상관없이 이름에 따라서 값을 줄 수 있게 된다.

```python
def plus(a, b):
    return a - b

result = plus(b=30, a=1)
print(result)
```