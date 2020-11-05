---
layout: post
title: 강의정리 03 - Logistic-regression
category: ML_Summary
tags: [ML]
comments: ML
---

# Logistic_Regression

- Linear_Regression에 sigmoid함수 씌운 모델

<center>
<figure>
<img src="https://imgur.com/G4riFgu.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 참, 거짓을 판별하는데 쓰인다.

<center>
<figure>
<img src="https://imgur.com/Htga3fL.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 시그모이드 함수를 썼으므로, 역함수인 로그의 모양인 `C(H(x), y) = -ylog(H(x)) - (1-y)log(1-H(X))`를 통해서 손실함수를 구한다.

# Multinomial_Regerssion

- 로지스틱에서 2개의 선으로 구분하는 아이디어를 Multinomial에 적용할 수 있다. Multinomial은 여러개의 클래스가 존재한다.

- Binary만으로도 Multinomial이 구현이 가능하다!

- 다층분류는 원핫인코딩으로 피드백을 준다.

<center>
<figure>
<img src="https://imgur.com/191cIOF.png" alt="views">
<figcaption>학습이란 2개의 선을 구분하는 것이다.</figcaption>
</figure>
</center>

<center>
<figure>
<img src="https://imgur.com/Ob5Bx7x.png" alt="views">
<figcaption>여러개의 선의 중첩이 Multinomial이 된다.</figcaption>
</figure>
</center>

<center>
<figure>
<img src="https://imgur.com/et7Xrqo.png" alt="views">
<figcaption>Weight의 값을 각가의 x1, x2, x3데이터에 대입함으로써 판별이 된다.</figcaption>
</figure>
</center>

# DeepLearning

- multinomial에서 썼던 H(x) = x1*w1 + x2*w2 + x3*w3 + b의 공식이 딥러닝에 그대로 적용된다.

- 딥러닝은 HiddenLayer의 출력층을 잘 정해주면 된다.