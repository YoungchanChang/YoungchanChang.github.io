---
layout: post
title: 강의정리 01 - Linear Regression
category: ML_Summary
tags: [ML]
comments: ML
---

# Machine Learning이란?

- 기존 프로그래밍은 y = W * x + b에서 **W와 b의 값을 사람이 정하는 것**이라면

- Machine Learning은 x와 y의 값들을 통해 **W와 b를 컴퓨터가 추론**하는 것이다.

<center>
<figure>
<img src="https://imgur.com/iKglIZT.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# HCG

- 컴퓨터는 W와 b의 값을 추론하기 위해 3단계를 거친다. 이 단계를 Hypothesis(가설) - Cost(비용) - Gradient Descent(경사 하강)의 3단계로 쓸 수 있다. W와 b의 값을 컴퓨터가 추론한 뒤에 얼마나 맞았는지 실제 결과값과 비교한 뒤, 값을 재조정하는 과정이다.

- W와 b에 대해서 문제를 푼뒤 실제 값으로 채점한 뒤 W와 b를 수정하는 과정의 반복이다.

<center>
<figure>
<img src="https://imgur.com/vJsfA7F.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### 다트에 비유하기

- 비유를 하면, 처음 다트를 던졌을 때로 비유할 수 있다. 간단히 x를 내 힘의 크기라고 하고, y를 다트 점수라고 하자. 나의 목표는 **얼마만큼의 힘을 줘야 다트 점수를 정확하게 받느냐**이다.

- 나는 처음에 눈을 가리고 다트를 던진다. 그리고 다트에 정중앙과 얼마가 차이나는지 계산한다. 힘을 더 세게줄지 약하게 줄지 결정한다.

- 그리고 다시 다트를 던지고 정중앙과 얼마나 차이가 나는지 계산하고 힘을 조절한다. 이 과정의 **반복이 컴퓨터의 학습 과정**이다.

### Hypothesis(가설)

- W값을 랜덤한 값으로 추론한다. (편의성 W와 b를 구해야 되지만 W하나만 두었다.)

- W값이 정답과 차이날수록 Cost가 많이 난다.

<center>
<figure>
<img src="https://imgur.com/6tIQpkS.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### Cost(비용)

- 가설이 얼마나 맞는지 검증한다. `cost = (1/m)*∑(H(xi) - yi)²` 모든 데이터(x)값들에 대해서 실제 값들과 차이를 구해야한다.

- 여기서 제곱을 하는 이유는 음수값이 나왔을 때 양수로 바꿔주기 위해서이다.

- 실제 데이터인 x의 값들이 커지면 cost값도 커진다.

```
# 비용함수(Cost) 요약
- 실제 값과 가설의 차이를 구하기 위한 함수
- 음수 값이 나왔을 때 양수로 구하기 위해서 제곱을 해준다.
- x의 값들이 커지면 Cost가 커진다.
- W의 값이 정답과 차이날 수록 Cost가 커진다.
```

- 비용함수는 W에 대한 2차함수 그래프로 그릴 수 있다.

<center>
<figure>
<img src="https://imgur.com/aTHPX9n.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### Gradient Descen Algorithm

- W가 한 점이 정해지면, 순간 변화율이 계산이 된다. 이 **순간변화율은 W값이 실제 값과 얼마나 차이나는지를 의미**하게 된다.

- 이 순간변화율에 내가 다음 단계로 넘어가게 하고 싶은 값(α=learning rate)만큼 을 곱해서 **원래 W값 재조정**한다.

<center>
<figure>
<img src="https://imgur.com/LYozxel.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### 순간변화율(미분값) 구하기

- 손실함수를 `cost = (1/m)*∑(H(xi) - yi)²`를 2로 나눈다. 2로 나누는 것은 편의를 위해서이다.

- `cost = (1/2m)*∑(H(xi) - yi)²`식에서 순간 변화율을 구하기 위해서 미분을 한다.

- 미분한 값에 대해서 학습 비율을 정한뒤 원래 W값에 추가한다. `W : = W - α * ( δ / δ * W ) * cost(W)`

- 2차함수에서 우측에 있으면 W값을 좌측으로 옮기고, 좌측에 있으면 우측으로 옮기게 된다.

- `( δ / δ * W ) * cost(W)`의 식 도출 과정은 아래와 같다. x와 y값이 주어졌을 때 **미분값은 하나의 상수처럼 취급**된다.

```
(H(xi) - yi)²
= (W*x - yi)²
= W²*x² - 2*W*x*yi + yi²
= (W값에 대해서 미분한다) 2*W*x² - 2 * x * yi
= 2(w*x - yi)*x
```
