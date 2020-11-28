---
layout: post
title: View에서 데이터 처리하기
category: webscraping
tags: [python, webscraping]
comments: python
---

# 사용

[Validate Everything](https://nomadcoders.co/airbnb-clone/lectures/1308)


# fieled 설정하기

- 아래와 같이 validator를 둘 수 있다.

```python
    accuracy = forms.IntegerField(max_value=5, min_value=1)
    communication = forms.IntegerField(max_value=5, min_value=1)
    cleanliness = forms.IntegerField(max_value=5, min_value=1)
    location = forms.IntegerField(max_value=5, min_value=1)
    check_in = forms.IntegerField(max_value=5, min_value=1)
    value = forms.IntegerField(max_value=5, min_value=1)
```