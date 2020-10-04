---
layout: post
title: 모두를 위한 딥러닝 28 - CNN Lab
category: ML
tags: [ML]
comments: ML
---

# CNN : Max pooling and others

- Convolution으로 값을 뽑아내고, 뽑아낸 값을 작게 subsampling을 한다. 세번째는 feature의 특징을 뽑아낸다.

<center>
<figure>
<img src="https://imgur.com/dLVjBdx.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- vector값들은 일반적인 forward neural net, fully connected network가 되어서 regression(**classification**할 수 있다.)

- CNN은 **이미지에 처리**에 특히 잘 작동한다.

- CNN은 주어진 이미지에 **fliter**를 두면서 각각 하나의 값을 뽑아낸다. 여러개로 움직이기 때문에 여러개 **convolution**값이 나오고 sampling을 거쳐서 subsampling으로 나눈다.

# 텐서플로우 예씨

- 3x3x1의 이미지가 있고, 2x2x1의 필터가 있을 때, stride 1x1로 하나의 값을 뽑아내는 과정을 거칠 수 있다. 여기에는 2x2에 색깔이 1개인 convolution data가 나온다.

<center>
<figure>
<img src="https://imgur.com/HMhsV09.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- matplotlib으로 보면 아래의 예시가 나온다. print(image.shape)의 값으로 (1, 3, 3, 1)이 나온다. 첫번째 값은 n개이고, 두번째와 세번째는 3x3을 의미하고 color 1개, **필터의 개수**를 의미한다.

- plt.imgshow를 통해서 이미지를 시각화한다. 3차원에 있지만 2차원으로 보여지게 된다.

```python
import tensorflow.compat.v1 as tf
tf.disable_v2_behavior()
import numpy as np
import matplotlib.pyplot as plt

sess = tf.InteractiveSession()
image = np.array([[[[1],[2],[3]],
                   [[4],[5],[6]], 
                   [[7],[8],[9]]]], dtype=np.float32)
print(image.shape)
plt.imshow(image.reshape(3,3), cmap='Greys')
```

- 필터가 2x2, 1개의 이미지, 몇개의 필터인지 명시한다. 필터를 그림 위에 올려놓고, 서로 마주보는 숫자끼리 곱해서 한 값을 뽑아낸다.

<center>
<figure>
<img src="https://imgur.com/whDhKlP.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 텐스플로우는 tf.nn.conv2d()에 이미지, weight을 넣고, sttride를 준 뒤에 padding을 주면 된다. padding은 convolution의 사이즈에 상관 없이 원래 이미지와 같게 해준다.

```python
# print("imag:\n", image)
print("image.shape", image.shape)
weight = tf.constant([[[[1.]],[[1.]]],
                      [[[1.]],[[1.]]]])
print("weight.shape", weight.shape)
conv2d = tf.nn.conv2d(image, weight, strides=[1, 1, 1, 1], padding='VALID')
conv2d_img = conv2d.eval()
print("conv2d_img.shape", conv2d_img.shape)
conv2d_img = np.swapaxes(conv2d_img, 0, 3)
for i, one_img in enumerate(conv2d_img):
    print(one_img.reshape(2,2))
    plt.subplot(1,2,i+1), plt.imshow(one_img.reshape(2,2), cmap='gray')
```

# Pooling

- 데이터를 줄여서 subsampling한다. **pooling은 convolution과 같은 개념**이다.

```python
image = np.array([[[[4],[3]],
                    [[2],[1]]]], dtype=np.float32)
pool = tf.nn.max_pool(image, ksize=[1, 2, 2, 1],
                    strides=[1, 1, 1, 1], padding='VALID')
print(pool.shape)
print(pool.eval())
```


# 참고

[보여주기](https://cs.stanford.edu/people/karpathy/convnetjs/demo/cifar10.html)