---
layout: post
title: 모두를 위한 딥러닝 12 - Softmax Regression
category: ML
tags: [ML]
comments: ML
---

# Logistic Regression

- Logitstic의 기본 개념은 Regression의 값이 다양하기 때문에 시그모이드 함수를 써서 **0과 1사이 값으로 압축**하는 것이다.

- Logistic의 가설은 자연상수 e의 값으로 여기서 역함수인 로그를 쓴다면 비용함수를 구할 수 있다.

- Logistic의 흐름

```
1. X의 데이터에 가중치를 둬서 H(x) = W*X로 만든다.
2. z = H(x), g(z)로 해당 함수에 시그모이드 함수를 씌운다.
3. 0과 1사이의 값이 나오게 된다.
```

- 보통 시스템을 통해 예측한 값은 **Y의 hat**이라고 표현한다. Y는 실제 데이터를 의미한다.

- W를 학습한다는 것은 2개를 구분하는 선을 찾아내는 것이다. 여러차원에 있게 된다.

<center>
<figure>
<img src="https://imgur.com/191cIOF.png" alt="views">
<figcaption>학습이란 2개의 선을 구분하는 것이다.</figcaption>
</figure>
</center>

# Multinomial Regression

- 로지스틱에서 2개의 선으로 구분하는 아이디어를 Multinomial에 적용할 수 있다. Multinomial은 여러개의 클래스가 존재한다.

- **Binary만으로도 Multinomial이 구현이 가능하다!**

- 여러개의 Binary를 겹치게 되면 Multinomial이 도게 된다.

<center>
<figure>
<img src="https://imgur.com/Ob5Bx7x.png" alt="views">
<figcaption>여러개의 선의 중첩이 Multinomial이 된다.</figcaption>
</figure>
</center>

- X가 주어졌을 때 A인지 아닌지, B인지 아닌지, C인지 아닌지 판별하는 classification을 갖고 구현이 가능하게 된다.

- Weight의 값을 각각의 x값에 줌으로써 판별식이 만들어진다. 판별식에 데이터를 곱한 값이 가설이 된다.

- 3개의 독립된 classification을 구현하면 3개의 독립된 가설이 나오게 된다.

- 각각에 sigmoid를 적용시킬 수 있다.

<center>
<figure>
<img src="https://imgur.com/et7Xrqo.png" alt="views">
<figcaption>Weight의 값을 각가의 x1, x2, x3데이터에 대입함으로써 판별이 된다.</figcaption>
</figure>
</center>

### probability

- Logistic classfifier을 주면 A와 B와 C에 해당하는 값들이 나오게 된다. 이 값의 합이 **1이 되게** 만드는 게 좋다.

- softmax함수를 이요한다. n개의 값을 softmax에 넣게 되면 probability가 나오게 된다.

- 특징 1.0~1사이의 값이고 2.전체의 sum이 1이 된다. 각각이 확률이 된다. 0.7, 0.2, 0.1이 되게 된다.

### cross-entropy Cost Functinon 설계하기

- 손실함수는 정답과 예측값을 주고 피드백을 받아야 한다.

- Label, 실제의 값 Y와 Y햇 사이의 차이가 얼마나 되는지 cross entropy함수를 통해 구하게 된다. 로그를 한 값을 곱하게 된다.

- cross entropy함수를 쓰면 여러개의 정답 중 맞는 정답은 0의 cost, 틀린 정답은 높은 cost를 갖게 된다.

- 이 과정에서 행과 열을 맞추기 위해 **원핫인코딩을** 사용한다.

<center>
<figure>
<img src="https://imgur.com/yOwsELo.png" alt="views">
<figcaption>원핫인코딩을 사용하면 정답에만 피드백을 줄 수 잇게 된다.</figcaption>
</figure>
</center>

### 원핫인코딩

- 값들에 대해서 1은 010000 / 7은 000010으로 바뀐다. 총 10개의 CASE중에 1개 ONE이 HOT 뜨게 만든다.

- 삼각형 0 사각형 1 원 2가 있다면 삼각형은 100 사각형은 010 원은 001로 바꾼다.

- softmax는 3개의 벡터를 형성하면 칸칸이는 0과 1사이의 실수가 나온다. 시그모이드와 다를 바가 없다. 다만 합하면 1이 되게 된다.

- 시그모이드로 하면 1.0 1.0 0.5로 되는데 softmax는 합이 1이 되게 된다.

- 0.1 / 0.2 / 0.7로 예측을 했을 때 정답은 0 / 0 / 1로 되어서 맞추고 틀리는 것에 대해서 피드백을 줄 수 있다.

- 따로따로 비교하기 위해서 전부 하나의 배열로 만든다. 이 과정이 원핫인코딩이다. 벡터별로 비교해서 loss를 계산하는 function인 categoriacl_crossentropy라고 한다.

# 참고

[원핫인코딩](https://www.youtube.com/watch?v=IPR2bYFa6Rw&list=PL9mhQYIlKEheoq-M4EifTMPNWMw7poclK&index=2) 9분과 24분