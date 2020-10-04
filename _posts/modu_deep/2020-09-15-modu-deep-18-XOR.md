---
layout: post
title: 모두를 위한 딥러닝 18 - XOR 문제 풀기
category: ML
tags: [ML]
comments: ML
---

# XOR문제

- one logistic regression unit은 절대 XOR을 풀 수 없다. 수학적으로 증명이 되었다.

- 만약에 2개 3개를 합치면 풀 수 있다.(MLPD)

- 각각의 복잡한 network에 들어간 weigth과 bias의 학습은 불가능 하다! -> backpropagation으로 해결했다.

### XOR이 Neural Network로 풀기

- Linear로는 XOR문제를 풀 수 없다.

- Neural Net은 하나의 Unit이 입력을 받는다. W*x + b로 하나의 값이 이루어진다.

- Neural Net을 여러개를 합치면 연결이 된다.

<center>
<figure>
<img src="https://imgur.com/QuU6wHX.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### Forward propagation

- weight를 가졌던 gate, perceptron이 들어가는 값이 뒤로 전달이 된다. 각각의 출력에 sigmoid가 다른 unit의 입력으로 들어가게 된다. 하나의 neural network로 볼 수 있다.

### NN

- K(x) = sigmoid(X*W1 + B1)

- Y = H(x) = sigmoid(k(x)*W2 + b2)

- 위의 식을 아래와 같이 표현할 수 있다.

```
K = tf.sigmoid(tf.matmul(X, W1) + b1)
hypothesis = tf.sigmoid(tf.matmul(K, W2) + b2)
```

<center>
<figure>
<img src="https://imgur.com/Pb1punP.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### backPropagation

- 기계적으로 학습하게 하기 위해서 G(Gradient Descent)알고리즘을 쓴다. Gradient Descent 경사 하강 알고리즘은 Cost Function에 미분한 값이다.

- Y햇값이 2차 cost함수 모양으로 만들어진다면, 그 점에서의 기울기를 구해서 Learning rate만큼 계속 내려가면 된다. 최종적으로 global minimum에 도달할 수 있다.

- Neural Network를 쓰게 된다면 여러 미분값이 포함되게 되면서 복잡하게 된다.

- **x1이 Y에 끼치는 영향**을 알아야 weight를 조절한다. 각각의 Node들이 Y에 미치는 영향을 알기에는 너무 계산값이 영향을 많이 미친다.예측값과 실제값을 구해서 cost값을 뒤에서부터 앞으로 돌려서 계산한다.

- 아래 그림에서 w가 최종 결과 f(x)에 **미치는 영향을 알기 위해 미분**을 하고, x가 f(x)에 **미치는 영향을 알기 위해 미분**을 한다.

<center>
<figure>
<img src="https://imgur.com/wA04c86.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


### Chain Rule 실습

- f = w*x + b, g = w*x => f = g + b

- w가 f에 미치는 영향, x가 f에 미치는 영향은 결국 미분값이 된다.

- Chain Rule은 굉장히 중요하다!!!

- 2가지 방법이 있다. 1.forward 실제 학습 데이터에 그래프에 값을 입력. 2. backward로 실제 미분의 값 계산

<center>
<figure>
<img src="https://imgur.com/lzEjVaY.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 위의 식을 미분할 때, θf/θg = 1 (f = g + b로 보았다, g자체를 변수로 보았다), θf/θb = 1

- f = w*x + b / g = w*x식이 있고, f(x)에 w가 미치는 영향을 알기 위해서는 **f(x)를 w로 미분**해야된다. θf/θw = (θf/θg)*(θg/θw)가 된다.

- 아래 그림을 해석하면 w를 미분한 값이 5가 나왔으면, w가 1만큼 바뀌면 f(x)는 5배가 바뀐다는 뜻이다. f의 출력에 대해서 조율이 가능하게 된다.

<center>
<figure>
<img src="https://imgur.com/39aKYIh.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### 복잡한 경우의 Back propagation

- 여러 Neuron이 연결된 경우, 가장 마지막부터 계산한다. a가 f에 미치는 영향을 θf/θa = 1이 된다.

- 제일 끝의 x의 값을 구하기 위해서는 θf/θx = (θf/θg)*(θg/θx)의 값을 구하면 된다. 중간에 많은 데이터들이 있어도 최종 출력값을 알 수 있다.

- 복잡한 식도 미분값을 통해서 구할 수 있다.

- 텐서플로우에서는 모든 것이 그래프이다.

- 텐서플로우는 각각을 그래프로 갖고있게 된다. 아래의 코스트함수의 미분값이 있다면 텐서플로우는 각각을 그래프로 만들었다. 빼고 Multi로 구한다. TensorFlow가 BackPropagation을 미분하기 위해서 구한 것이다.

<center>
<figure>
<img src="https://imgur.com/A1n9RtM.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 기계적으로 아무리 복잡해도 Back propagation으로 기울기로 미분값을 구할 수 있다.

