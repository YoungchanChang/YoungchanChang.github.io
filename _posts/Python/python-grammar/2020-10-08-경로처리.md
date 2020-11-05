---
layout: post
title: kwargs
category: python
tags: [python, dictionary]
comments: true
---

# 플라스크 서버 구동시 유의사항

# 플라스크에서 상위 디렉터리 이용할 때

- sys.path를 붙이면 된다.

```python
import os,sys
import traceback
sys.path.append(os.path.dirname(os.path.abspath(os.path.dirname(os.path.abspath(__file__)))))
print(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
print(os.path.abspath(os.path.dirname(os.path.abspath(__file__))))
print(os.path.dirname(os.path.abspath(os.path.dirname(os.path.abspath(__file__)))))
print(sys.path.append(os.path.dirname(os.path.abspath(os.path.dirname(os.path.abspath(os.path.dirname(os.path.abspath(__file__))))))))
```

[참고](https://brownbears.tistory.com/296)

# 에러코드

- ValueError: attempted relative import beyond top-level package

- 디렉터리가 아닌 패키지를 이용하면 된다.

# Absolute Path(절대 경로)

- 프로젝트의 가장 최상위 디렉토리에서 경로에서 시작

# Relative Path(상대 경로)

- from . import class1

# 딕셔너리 안에서 정렬하기

[참고](https://wayhome25.github.io/python/2017/03/07/key-function/)

# 참조

[스택오버플로우](https://stackoverflow.com/questions/8706309/how-to-reference-to-the-top-level-module-in-python-inside-a-package)

[공식문서](https://docs.python.org/3/reference/import.html)

[파이썬 디렉터리](https://velog.io/@devmin/%ED%8C%8C%EC%9D%B4%EC%8D%AC-import%EA%B0%80-module%EA%B3%BC-package-%EB%A5%BC-%EC%B0%BE%EC%95%84%EA%B0%80%EB%8A%94-%EA%B2%BD%EB%A1%9C)

[파이썬~](https://m.blog.naver.com/wideeyed/221839634437)
