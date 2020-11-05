---
layout: post
title: 파이썬 장고 os_path
category: Django
tags: [python, Django]
comments: Django
---

> [참고](https://brownbears.tistory.com/296)

# os_path는 언제 쓰이는가?

- 예전에 상위 디렉터리를 이용하려고 했는데, 상위 디렉터리를 인지하지 않아서 애를 먹은 적이 있다. 그 때 썼던 방법이 아래와 같이 시스템 경로에서 인지하게 하는 것이었다.

```python
import os,sys
sys.path.append(os.path.dirname(os.path.abspath(os.path.dirname(os.path.abspath(__file__)))))
print(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
```

### 장고에서 os_path와 관련된 내용

- `BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))`
    - 파일에 대해서 얻은 디렉토리를 얻은 것을 기본 디렉토리로 설정한다.

```console
>>> os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
E:\GitHub\django_aribnb_again

>>> os.path.dirname(os.path.abspath(__file__))
E:\GitHub\django_aribnb_again\config\

>>> os.path.abspath(__file__)
E:\GitHub\django_aribnb_again\config\settings.py
```

- 특정 경로에 대해 절대 경로 얻기	os.path.abspath(".\\Scripts")
    - "C:\Python35\Scripts"

- 경로 중 디렉토리명만 얻기	os.path.dirname("C:/Python35/Scripts/pip.exe")
    - "C:/Python35/Scripts"

- 경로를 병합하여 새 경로 생성	os.path.join('C:\Tmp', 'a', 'b')
    - "C:\Tmp\a\b"
