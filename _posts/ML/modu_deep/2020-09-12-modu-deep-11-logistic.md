---
layout: post
title: 모두를 위한 딥러닝 11 - Logistic(regression) Algorithm
category: ML
tags: [ML]
comments: ML
---

# Logistic Algorithm

### Logistic Algorithm이란

- 분류 알고리즘중에 정확도가 높은 알고리즘, Neural Network과 Deep Learning에 중요한 알고리즘

- 사용 용도] 스팸 감지 : 스팸메일인지 아닌지 / 페이스북 피드 : 친구들에게 보여줄지 안 보여줄지 / 신용카드 사기 거래 : 평소 패턴과 달라서 사기거래인지 아닌지

- Radiology 이미지를 보고 나쁜 tumor인지 괜찮은 tumor인지 확인한다. 주식을 보고 살까 팔까결정한다.

### Logistic Algorithm에서 시그모이드 함수 사용 이유

- **참, 거짓을 판별하는데 Linear regression**은 적합하지 않다. x에 대해서 y의 값을 내놓았을 때 y는 참과 거짓이 아니다. y의 특정 지점이상(ex) 0.5.이상일 때)을 참과 거짓으로 판별하게 되면, 매우 큰 값이 왔을 때 기울기가 달라져서 y값을 재조정해야 되는 문제(ex) 0.4이상일 때)가 문제가 된다.

- 또한 0과 1만이 필요한데 0과 1이외의 값들이 나온다.

- Linear Regression을 **0과 1사이로 압축을 시켜주는 형태의 함수**가 필요하게 된다.

- 위 함수를 **시그모이드 함수**라고 한다. 시그모이드 함수는 오른쪽과 같다. `g(z) = 1/(1 + e^(-z))`

- z값을 입력을 받으면 0인지 1인지 판별할 수 있게 된다.

<figure>
<img src="https://imgur.com/CChMbNr.png" alt="views">
<figcaption>z값에 따라 0과 1만을 반환할 수 있게 된다.</figcaption>
</figure>
</center>

- Linear Regerssion에서 컴퓨터는 가설을 세울 때 H(x) = W*x + b에서 W와 b의 값을 목표로 했다면, Logistic에서 `H(x) = 1/(1 + e^(-WTX)`식에서 W와 t의 값을 구하는 것을 목표로 한다.

### Cost Function

- Linear Regression은 가설인 `H(x) = W * x  + b`의 손실함수로 `cost = (1/m)*∑(H(xi) - yi)²`를 썼다. 이 함수는 어느 지점을 쓰던 최소점에 도달할 수 있도록 한다. 그런데 Logistic에서는 2차함수를 쓴다면 0과 1의 값밖에 없기 때문에 함수가 울륵불륵한 모양이 된다.

- 울륵불륵한 함수의 문제점은 최소점을 찾기 어렵다는 것이다. 그렇기 때문에 새로운 최소점을 찾는 함수가 필요하게 된다. global minimum을 찾기 힘들게 된다. 모델이 나쁘게 Prediction되게 된다.

- 따라서 Logistic Function아 Cost Function은 `c(H(x), y) {-log(H(x)) : y = 1 , -log(1 - H(x)) : y = 0}`를 값으로 만든다. y가 0일때와 y가 1일때로 나뉘어서 평가를 하게 된다. 자연상수 e와 반대되는 log를 쓰는 것이 기본적인 아이디어이다.

- g(z) = -log(z)일 때, z가 1보다 큰 값은 나올 수가 없다. z가 0에 가까워지면 함수는 매우 커진다.

- cost함수의 의미는 실제 값과 예측한 값이 같거나 비슷하면 cost값이 작아지고, 크게 틀리면 cost함수에게 벌을 주게 된다. y=1인 경우, H(x)의 예측이 1이라면, cost는 0에 가깝게 된다. H(x) = 0이고, cost값이 0이라면 값이 무한대에 가깝게 된다. 예측이 틀리면 cost가 굉장히 높아지게 된다.

- y의 실제 label이 0인데, 예측이 0이라면 값이 0에 가깝고 1이라면 무한대에 가까워지게 된다.  

- 이 두함수를 붙이면 2차함수같은 곡선의 모양이 나오게 된다.

- 조건을 합친 식은 오른쪽과 같다. `C(H(x), y) = -ylog(H(x)) - (1-y)log(1-H(X))`y=1일때 c는 `-log(H(x)) : y = 1`값만 남고, y=0일때는 `-log(1 - H(x)) : y = 0`값만 남는다.

- 이차함수모양임으로 경사타기 내려가기를 할 수 있다. 기울기를 구하기 위해서 미분을 하게 된다. `W : = W - α * ( δ / δ * W ) * cost(W)`

```
#cost function
cost = tf.reduce_mean(-tf.reduce_mean(Y*tf.log(hypothesis) + (1-Y)*tf.log(1-hypothesis)))

#Minimize
a = tf.Variable(0.1) #Learning rate, alpha
optimizer = tf.train.GraideintDescentOpimizer(a)
train = optimizer.minimize(cost)
```

### 결과값

```python
# Hypothesis
hypothesis = tf.matmul(X, W) + b
# Simplified cost/loss function
cost = tf.reduce_mean(tf.square(hypothesis - Y))


# Hypothesis using sigmoid: tf.div(1., 1. + tf.exp(tf.matmul(X, W)))
hypothesis = tf.sigmoid(tf.matmul(X, W) + b)
```

- Linear Regression은 제곱해서 평균값을 구한 것이 비용함수였다면,

- Logistic은 H(x) = W * x + b를 시그모이드 함수에 넣은 값이 비용함수이다.


### 추가로 알아두면 좋은 사실

- 음수를 취하는 이유는 아래 그래프와 같다.

<center>
<figure>
<img src="https://imgur.com/q5d5xgg.png" alt="views">
<figcaption>-log(H(x))</figcaption>
</figure>
</center>






