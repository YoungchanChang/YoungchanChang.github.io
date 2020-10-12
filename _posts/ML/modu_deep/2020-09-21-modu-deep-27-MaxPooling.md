---
layout: post
title: 모두를 위한 딥러닝 27 - ConvNet Max Pooling과 Full Network
category: ML
tags: [ML]
comments: ML
---

# CNN : Max pooling and others

- Convolution과 RELU가 붙어있고 중간에 POOLING을 한 번씩 하게 된다.

<center>
<figure>
<img src="https://imgur.com/UUtYlOU.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# Pooling layer(sampling)

- 한 레이어만 뽑아내면 특정한 Layer가 나온다. 보통 이미지를 갖고 resize를 하면 사이즈가 작아지게 된다. **사이즈를 작게 만드는 것**을 pooling이라고 한다.

- 풀링한 것을 샘플링한 것을 모아서 다음 단계로 넘긴다.

- 4x4의 이미지가 있을 때 필터를 쓴다. stride가 2라면 2칸씩 움직인다. 2칸씩 내려가게 되다보면, 2x2의 아웃풋이 나온다.

- 값을 옮기는 여러가지 방법 중에 가장 큰 값을 고르는 MAX POOLING을 이용하게 된다. 샘플링이라고 부르는 이유는 **전체 값 중에 한개만 뽑는다**.

- RELU라는 Function에 입력한다. POOLING 샘플링을 하게 된다.  원하는 대로 쌓아가면 된다. 정하는 형태로 구성을 하면 된다. 마지막에 POOLING을 한 값이 있다.

- 원하는 만큼의 neural network에 넣은 뒤에 하나의 label을 고르게 된다.

# CNN 활용 예

- 라쿤의 설계도는 32X32 INPUT이 주어지면, 6개의 filter로 Convolution이 이루어진다.

<center>
<figure>
<img src="https://imgur.com/GKmW7dp.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- AlexNet의 예시. 277x277x3의 이미지 레이어를 받는다. 96개의 필터를 받은 뒤에 11x11x3의 필터를 써서 4개의 스트라이드를 쓴다.

<center>
<figure>
<img src="https://imgur.com/SrB6Ijy.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 계산을 하면 55x55x96이 나온다. 35K파라미터가 필요하다.

- 두번째는 POOLING Layer를 쓴다. 3x3필터를 쓴 뒤 stride 2를 쓴다.

- 최종적으로 나온 값을 fully Connected Network에서 4096의 출력을 쓴다. 4096의 입력을 받아서 4096의 출력을 보낸다. 이미지 1000개를 비교한다.

- GoogleNet이 있다. Inception module은 입력에 대해서 병렬적으로 쓰고 pooling을 한다. 레고를 쌓는 구조를 쓴 뒤 deep하게 들어갔다.

<center>
<figure>
<img src="https://imgur.com/rPTcs67.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


- ResNet등장. AlexNet은 8개의 Layer을 쓰고 152개의 Layer을 쓴다. Layer를 152개를 쓰면 학습하기가 어려워질 수 있다. Fast Forward로 문제를 해결했다. 

<center>
<figure>
<img src="https://imgur.com/6enhcg1.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 값이 점프가 되어서 합쳐짐으로, 깊이가 낮아질 수 있다.

# 응용

- Setence Classification으로 문장 분류도 한다.

<center>
<figure>
<img src="https://imgur.com/6enhcg1.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


# 참고

[보여주기](https://cs.stanford.edu/people/karpathy/convnetjs/demo/cifar10.html)