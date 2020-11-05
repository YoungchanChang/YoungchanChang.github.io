---
layout: post
title: 강의정리 02 - Multi-variable
category: ML_Summary
tags: [ML]
comments: ML
---

# Multi-variable

- 가설 y = W * x + b에서 x의 값 하나로 y의 값을 예측했다. 여기서 변수가 2개가 된다면 어떻게 될까?

###

- 변수가 2개인 경우는 y = w1 * x1 + w2 * x2표현할 수 있다. 이 것이 **조금 더 복잡해진 것이 Multinomial Regression**이다.

<center>
<figure>
<img src="https://imgur.com/Sy1VjvS.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 비용함수의 그래프는 아래와 같다.

<center>
<figure>
<img src="https://imgur.com/LJN0iHx.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


### 추가로 공부해야되는 사항

- 미분을 했을 때 결과에 미치는 영향(이 부분은 Vanishing Gradient)

- Multinomial(이 부분은 딥러닝의 여러 부분을 이해할 수 있게 한다.)


# 참조 사이트

[변수 2개 그래프](https://www.geogebra.org/3d?lang=ko)