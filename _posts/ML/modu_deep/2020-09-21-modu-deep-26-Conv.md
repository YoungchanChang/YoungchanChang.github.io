---
layout: post
title: 모두를 위한 딥러닝 26 - CNN의 Conv 레이어 만들기
category: ML
tags: [ML]
comments: ML
---

# CNN의 Conv 레이어 만들기

- 전체가 쭉 연결된 네트워크를 Fully connected Network라고 부른다.

- 입력을 여러개로 나눈 뒤, 이것을 하나로 합치고 앞으로 전달할 수 있다. Convolution Neural Network의 기본적인 아이디어이다.

- 기본적인 아이디어는 고양이가 특정 부분의 그림에서만 반응한다는 것을 알게 되었다. 일정 부분이 있으면 **그것만 바라보는 뉴런**이 있었다. 입력을 나누어 받는다.

<center>
<figure>
<img src="https://imgur.com/JzfBJwO.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


- 이미지를 잘라서 각각의 입력으로 넘기게 된다. 해당 층을 Convolution Layer라고 한다. Convolution을 여러번 하고 POOLING을 반복하게 되면, 마지막에는 Fully Connected Neural Network를 구해서 Labeling을 할 수 있게 된다.

<center>
<figure>
<img src="https://imgur.com/518h0wO.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# Start with an image

- 이미지가 32x32x3(RGB)층으로 갖고 있다고 하자. 이미지 하나를 처리를 할 때 **filter로 처리**한다. 필터의 크기는 내가 정의할 수 있다.

- 필터는 궁극적으로 한 값을 만들어낸다. 5x5를 x라고 했을 때, x를 입력받아서 처리를 한 후에 한 점만 뽑아낸다

- 한개의 값으로 만드는 것은 **Wx+b를 사용**하면 된다.

- w1* x1, w2 *x2, w3 *x3, w4 * x4를 하나의 값으로 만들어서 하나의 숫자로 만들어낸다. weight이 필터의 값이 된다. ReLU를 붙이면 ReLU창이 생기게 된다.

<center>
<figure>
<img src="https://imgur.com/eGjSP9H.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 똑같은 필터(w)에 대해서 다른 부분의 이미지도 보면 된다. 옆으로 넘기면서 **점차적으로 그림을 보듯이 옆으로 값을 넘긴다**.

<center>
<figure>
<img src="https://imgur.com/IEWeHxj.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 전체 이미지를 훑은 다음에 **한 값을 가져오게 된다**. 모아지는 값은 기본적인 산수이다.

- 7x7size에서 3x3필터를 쓴다면 5x5의 사이즈가 나온다. 한 칸씩 옆으로 움직이는 것을 stride라고 부른다. stride:1은 한 칸씩 움직인다. 

<center>
<figure>
<img src="https://imgur.com/c39JFea.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- stride:2는 두 칸씩 움직인다. stride가 2라면 2칸씩 움직이기 때문에 3x3의 아웃풋이 생긴다.

<center>
<figure>
<img src="https://imgur.com/ZHg6gPx.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 아웃풋사이즈는 (N-F) / stride + 1이 된다.

<center>
<figure>
<img src="https://imgur.com/7vcwpoR.png" alt="views">
<figcaption></figcaption>
</figure>
</center>


# Padding

- 이미지가 CNN을 지날 때마다 작아지기 때문에 PADDING을 쓴다. 0이 가상적으로 있다고 가정한다. 그림이 급격하게 작아지는 것을 방지하고, 마지막이 모서리라는 것을 네트워크에 알려주는 것이다.

<center>
<figure>
<img src="https://imgur.com/rf7HIJl.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 32x32x3이미지가 5x5x3의 필터를 여러 번 거치게 할 수 있다. 필터를 6개를 동시에 적용시킨다면 갚이 달라진다. 6개의 필터를 적용시킨다면 깊이는 6이 된다. 전체 이미지, 나의 필터 사이즈에 따라 다음 이미지가 계싼된다. (x층, y층, 필터 수)로 계싼될 수 있따.

<center>
<figure>
<img src="https://imgur.com/HAK9kTC.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 이미지를 conv와 relu를 여러번 거치게 할 수 있다.

- 앞의 깊이에 따라서 뒤 층의 깊이가 결정된다.

# Convolution의 뜻

- convolution : 합성곱. 두 함수 중 하난를 반전(reverse)하고 이동(shift)시켜가며 다른 하나의 함수와 곱한 결과를 적분한다.

- Convolved Featrue은 합성곱 계층의 입출력 데이터를 특징맵(feature map)이라고 부른다. 그리고 딥러닝에서는 이미지 내에서 feature을 뽑기 위한 용도로 연산을 활용한다. Feature Detector의 각 kernel이 곱한 결과를 합하게 되고, 그 결과가 하나를 채우게 된다. 얻어낸 Feature중에서 가장 중요한 Feature을 뽑아내고, 이를 위해서 학습하는 역할을 CNN중 Convolutional Layer에서 수행한다.

# 참고

[CNN레이어](https://www.youtube.com/watch?v=Em63mknbtWo&list=PLlMkM4tgfjnLSOjrEJN31gZATbcj_MpUm&index=35)

[Convolved 뜻](https://umbum.dev/223)

[동영상으로 보는 Convolution image](https://www.youtube.com/watch?v=8rrHTtUzyZA&list=WL&index=4&t=526s&app=desktop)