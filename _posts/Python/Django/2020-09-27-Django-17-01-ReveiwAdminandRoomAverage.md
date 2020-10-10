---
layout: post
title: 파이썬 장고 Reveiw Admin and Room Average
category: Django
tags: [python, Django]
comments: Django
---

# Review Admin and Room Average

- **admin에서 메소드를 생성할 수 있었지만, model에서도 생성**할 수 있다.

- function을 이용하면 내부 정보로 **새로운 정보**를 만들 수 있다. 룸을 리뷰한 것들의 평균을 구할 수 있다.

### models안에 메소드를 넣기

- **admin에서 메소드를 생성할 수 있었지만, model에서도 생성**할 수 있다.

- reviews의 **평균**을 얻어야 한다. 평균은 admin에서만 쓰이는 것 뿐만이 아니라, **리뷰와 관련된 모델을 쓰는 모든 사이트에서 이용**할 수 있어야 한다.

- __str__을 list_display에 쓸 수 있다. 또 custom 함수를 모델에다 생성할 수 있다.

- 모델의 기능을 admin, 프론트, 콘솔에 쓰고 싶으면 모델에다 정의할 수 있다. short_description을 쓸 수도 있다.

- 모델 안에서 평균 구하는 함수 정의하기

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


# 클래스의 메소드를 언제쓸까?

- 주어진 데이터로 뭔가를 추가해서 보여줘야될때 ex> 평균, 진행중인지