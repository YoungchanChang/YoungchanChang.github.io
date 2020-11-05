---
layout: post
title: 모두를 위한 딥러닝 22 - sigmoid보다 relu
category: ML
tags: [ML]
comments: ML
---

# Let's go deep & wide!

- XOR문제를 풀기 위해서 각 유닛에 대해서 sigmoid가 있는데, 이 **sigmoid를 Activation function**이라고 부른다. 하나의 값이 전달 될 때 어느 값 이상이면 Active가 되고 어느 값 이하면 Active가 되지 않기 때문에 Activation function이라고 부른다.

- 아래 예시에서 layer가 다음 layer에 주는 output을 적은 값은 bias와 똑같이 쓴다. bias는 x변수에 추가된 변수처럼 쓰인다.

- 각 층마다 다음 층으로 넘겨진다. 체인처럼 연결된다.

```python
W1 = tf.Variable(tf.random_normal([2, 10]), name='weight1') #여기에 출력값 10이
b1 = tf.Variable(tf.random_normal([10]), name='bias1')  # 여기에도 똑같이 적용된다.
layer1 = tf.sigmoid(tf.matmul(X, W1) + b1)

W2 = tf.Variable(tf.random_normal([10, 10]), name='weight2')
b2 = tf.Variable(tf.random_normal([10]), name='bias2')
layer2 = tf.sigmoid(tf.matmul(layer1, W2) + b2)

W3 = tf.Variable(tf.random_normal([10, 10]), name='weight3')
b3 = tf.Variable(tf.random_normal([10]), name='bias3')
layer3 = tf.sigmoid(tf.matmul(layer2, W3) + b3)
```

- 앞에 있는 것(W1)을 input layer로 하고 맨 마지막에 결과(W3)를 output layer라고 한다. 안에 보이지 않는 것들(W2)은 hiddenlayer라고 한다.

# Vanishing gradient

- Layer의 층이 깊어졌는데 학습이 제대로 일어나지 않는 현상이 있게 된다. 이유는 BackPropgataion때문이다.

- f(x)최종 값을 알기 위해서 각각의 미분 값을 구하면서 W*x + b에서 x와 w값들을 전부 미분을 했다.

- 미분을 하면 x의 미분값은 W에 영향을 받는다. 해당 W의 값은 0~1사이의 값을 갖고 있게 된다.

- 작은 sigmoid를 통과하면 항상 1보다 작은 값이 되고, 경우에 따라서 0.01들이 chain rule로 곱해지게 된다. 마지막엔 매우 작은 값이 되게 된다.

- 뒤로 갈 수록 곱해지는 항이 많아지기 때문에 최종 미분값은 0에 가깝게 된다.

<center>
<figure>
<img src="https://imgur.com/nRNFWcc.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- Vanishing gradient. 경사기울기가 사라진다고 한다. 최종단 경사 기울기가 깊어질 수록 경사도가 사라지게 된다.

<center>
<figure>
<img src="https://imgur.com/86qUd5Z.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# sigmoid보다 relu(Rectified Linear Unit)가 좋은 이유

- 시그모이드는 항상 1보다 작은 값을 곱해나가니깐 최종값은 1보다 작아지게 된다. 아주 간단하게 ReLu를 만들었따.

- 0보다 크면 갈 때까지 가고, 0보다 끄면 작아버린다.

- sigmoid대신 relu를 쓰면 된다!!

- 마지막단은 0~1사이여야 되기 때문에 sigmoid를 쓰면 된다.

<center>
<figure>
<img src="https://imgur.com/4VEwB7S.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# Activation Functions

- ReLU이외에 많은 함수들이 생겨났다.

<center>
<figure>
<img src="https://imgur.com/oWHCrPz.png" alt="views">
<figcaption></figcaption>
</figure>
</center>