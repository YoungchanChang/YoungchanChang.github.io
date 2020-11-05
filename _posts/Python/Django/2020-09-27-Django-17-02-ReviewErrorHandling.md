---
layout: post
title: 파이썬 장고 ReviewErrorHandling
category: Django
tags: [python, Django]
comments: Django
---

# 아래 코드에서 에러

- 만약에 사용자가 방을 먼저 등록하고, 리뷰가 하나도 없다면 all_ratings=0가 됩니다. 그러면 아래 코드에서 그러면 len(all_reviews)는 0임으로 ZeroDivisionError를 발생시킵니다.

```python
    def __str__(self):
        return self.name

    def total_rating(self):
        all_reviews = self.reviews.all()
        all_ratings = []
        for review in all_reviews:
            all_ratings.append(review.rating_average())
            print(review.rating_average())
        return 0
```

### 에러 핸들링의 방법

- SOL1) 에러코드를 try-except로 감싸면 됩니다.

```python
        try:
            all_ratings = 0
            for review in all_reviews:
                all_ratings += review.rating_average()
            return all_ratings / len(all_reviews)
        except ZeroDivisionError:
            return 0
```

- SOL2) all_review가 0일때 if else로 감싸면 된다. 그런데 위에 코드가 더 좋다.

```python
    if all_reviews:
        all_ratings = 0
        for review in all_reviews:
            all_ratings += review.rating_average()
        return all_ratings / len(all_reviews)
    else :
        return 0
```
