---
layout: post
title: 모두를 위한 딥러닝 29 - Mnist
category: ML
tags: [ML]
comments: ML
---

# MNIST실습하기

- 28x28의 한 색깔의 이미지, COLOR은 1로 신경써서 줘야한다.

- 몇 개의 필터를 사용할 것인지도 정한다. stride는 2칸씩 옆으로 움직이겠다.

- 그리고 그림을 출력한다. maxPooling하면 이미지가 작아진다.

```python
sess = tf.InteractiveSession()

img = img.reshape(-1,28,28,1)
W1 = tf.Variable(tf.random_normal([3, 3, 1, 5], stddev=0.01))
conv2d = tf.nn.conv2d(img, W1, strides=[1, 2, 2, 1], padding='SAME')
print(conv2d)
sess.run(tf.global_variables_initializer())
conv2d_img = conv2d.eval()
conv2d_img = np.swapaxes(conv2d_img, 0, 3)
for i, one_img in enumerate(conv2d_img):
    plt.subplot(1,5,i+1), plt.imshow(one_img.reshape(14,14), cmap='gray')
```

# MNIST -deep

- N개의 입력에 784비트로 만든다. 이미지로 넣기 위해서 reshape을 한 번 해준다. 28*28이미지를 1개의 색깔, n개(-1)로 넣어준다. 28x28x1이미지라고 reshape을 해준다. 이게 입력이 된다.

```python
# input place holders
X = tf.placeholder(tf.float32, [None, 784])
X_img = tf.reshape(X, [-1, 28, 28, 1])   # img 28x28x1 (black/white)
Y = tf.placeholder(tf.float32, [None, 10])
```

- x의 이미지로 첫번째 convolution layer을 통과시킨다. N개가 들어왔을 때 3x3사이즈의 32개의 필터를 사용한다. conv2d하고 (x_imge, W1, strides=[1,1,1,1], padding='SAME') 스트라이드와 상관없이 입력의 이미지 사이즈를 같게 한다.

- 3 by 3 색깔은 1개 32개의 필터 (tf.random_normal([3, 3, 1, 32])

- 필터를 32개를 사용했기 때문에 32개의 이미지가 생성된다.

```python
# L1 ImgIn shape=(?, 28, 28, 1)
W1 = tf.Variable(tf.random_normal([3, 3, 1, 32], stddev=0.01))
#    Conv     -> (?, 28, 28, 32)
#    Pool     -> (?, 14, 14, 32)
L1 = tf.nn.conv2d(X_img, W1, strides=[1, 1, 1, 1], padding='SAME')
L1 = tf.nn.relu(L1)
L1 = tf.nn.max_pool(L1, ksize=[1, 2, 2, 1],
                    strides=[1, 2, 2, 1], padding='SAME')
L1 = tf.nn.dropout(L1, keep_prob=keep_prob)
```

- 두번째 레이어에서 입력값은 필터에서 3by3이미지, 32개의 컬러, 64개의 필터가 생긴다.

- CNN을 통과시키면 14,14, 64개가 된다. strides가 2by2이기 때문에 사이즈는 7이 된다. 

# deep CNN

- 기계적으로 연결만 해주면 된다.

- 기계적으로 연결해서 Deep해지면 정확도가 높아진다.

- Dropout할 때는 반드시 0.5나 0.7로 하고, 테스트할 때는 1로 해야한다.

# 참고
