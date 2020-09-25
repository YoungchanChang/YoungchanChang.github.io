---
layout: post
title: 모두를 위한 딥러닝 29 - RNN
category: ML
tags: [ML]
comments: ML
---

# RNN

### Sequence data(음성인식, 자연어)

- 하나의 데이터가 아니라 sequence로 되어있다. 하나의 단어를 본다고 맥락을 이해하는 것이 아니다. 이전에ㅔ 했던 단어들을 전부 이해해야 된다. sequence data이다.

- 기존에 있는 cnn같은 경우 하나의 입력이 있을 때 바로 출력이 되는 형태였다. (X -> Y)

- **이전에 있던 결과가 그 다음에 영향**을 미쳐야 된다.

- X가 계산한 Y가 그 다음 state에 영향을 미친다. 이전의 연산들이 영향을 미치게 된다.

<center>
<figure>
<img src="https://imgur.com/fW0bGzM.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### RNN

- state를 먼저 계산한 뒤 y를 다시 계산한다. 이전에 stae(h(t-1))이 입력으로 사용된다. x라는 입력값과, 이전에 있는 RNN셀에 나오는 값을 h(t-1)을 갖고 h(t)를 계산한다. x와 h(t-1)을 이용해서 연산을 한다.

<center>
<figure>
<img src="https://imgur.com/QxzznK6.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- RNN은 이전의 값과 현재의 값을 이용하는 Function이 모든 RNN을 통한다. 마치 전체가 하나와 같게 움직이게 된다. RNN의 값들을 계산하는 방법중 Vanilla Rnn의 연산방법은 아래와 같다.

```
h(t) = fW(h(t-1), x(t))
h(t) = tanh(W(hh)*h(t-1) + W(xh)x(t))
y(t) = W(hy)*h(t)
```

<center>
<figure>
<img src="https://imgur.com/wqoCC9M.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- y가 몇 개의 값으로 나올 것인가는 W의 형태에 따라 달려있다. **W의 벡터의 값**에 따라 달려있다.

### 예제(Character-level language model)

- "hello"를 하나의 입력으로 넣는다.

- h를 입력했을 때 e가 나와야되고, e가 나오면 l이 출력되어야 하고, l이 들어가면 l이 출력되어야 한다.

- 마치 네이버 **연관검색어**과 같다. 홍콩->김성훈. 단어가 아니라 글씨 레벨에서 예측한다. 현재 글씨가 있을 때 다음 글자가 뭘까 예측한다.

- hello를 원핫인코딩으로 표현한다. 케릭터를 **벡터로 표현**해야된다.

<center>
<figure>
<img src="https://imgur.com/2YGBFqh.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

```
h(t) = tanh(W(hh)*h(t-1) + W(xh)x(t))
```

- 전에 있던 h(t-1)이 없으므로 0이라고 둘 수 있다.

- 그 다음  ceel은 2개의 값들을 모두 연산한다. RNN은 이전의 것들을 기억한다.

- y를 뽑아낼때는 state에 값을 곱하게 된다. 결과를 뽑아낼 수 있게 된다. W의 shape에 따라 결정이 된다.

- Softmax를 취하게 되면 값을 비교할 수 있게 된다.

<center>
<figure>
<img src="https://imgur.com/ZJaJd5n.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### RNN의 활용

- one to one : Vanilla Neural Networks

- one to many : Image Captioning(image->sequence of words)
    - 이미지를 주면 나는 모자를 쓰고있다 등의 시리즈로 뽑을 수 있다.

- many to one : Sentiment Classification(sequence of words -> sentiment)
    - 문장을 보고 기쁘다, 슬프다 판단.

- many to many : Machine Translation(seq of words -> seq of words)
    - 문장을 입력 받고, 새로운 문자열로 출력한다.

- many to many(Video Classification on frame lvel)
    - 비디오의 여러 프레임을 받ㅇ른 뒤 출력을 설명한다.

<center>
<figure>
<img src="https://imgur.com/3HU4aWh.png" alt="views">
<figcaption></figcaption>
</figure>
</center>