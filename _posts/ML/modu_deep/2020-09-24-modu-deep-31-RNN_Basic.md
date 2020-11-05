---
layout: post
title: 모두를 위한 딥러닝 30 - Basic
category: ML
tags: [ML]
comments: ML
---

# RNN

- 이번 아웃풋이 다음 cell로 연결된다. 2가지로 나누어서 구현하면 된다. cell을 만들 때, 어떤 형태의 cell을 만들 것인가 결정한다. cell에서 나가는 output 출력의 크기가 얼마일지 정한다. hidden_size나 num_units라고 정한다.

- 만든 cell을 구동을 할 출력값을 정한다. tf.nn.dynamic_rnn으로 구현한다. cell과 원하는 입력데이터를 넘겨준다.

- _states의 값은 주로 output으로 많이 사용한다.

- 셀 생성과 구동하는 부분을 나눔으로써 cell부분을 바꿀 수 있다.

### One node

- 4(input-dim) in 2 (hidden_size)

- hello를 One hot encoding으로 벡터로 표현한다. 입력의 dimension은 4가 된다.

- output_size는 내 마음대로. **hidden_size에 따라서** 출력이 정해진다. 입력 데이터에 상관없이 dimension을 2개로 줄 수 있게 된다.

- x_data = np.array로 입력데이터를 넣는다.

- rnn이 어떤 출력을 내놓는지 본다. sess.runn()으로 initializer한 뒤에 출력을 한다.

- 어떤 shape이 나왔는지 보는게 중요하다.

- Sequence Data는 serize를 얼마나 받을까? 2번째 데이터가 된다. sequence_length 하나를 몇 번 받을것인가, 펼칠 것인가.

- 입력 데이터의 모양에 따라 결정된다. sequence가 5라면 1, 5, 4가 된다. 똑같은 출력값으로 나올 수 있다.

### Teach RNN 'hihello'

- hihello를 입력하면 다음 문자를 예측하게 학습시킨다.

- h를 입력을 했을 때 어떤 때는 i가 나와야하고 어떤 때는 e가 나와야한다. 이전의 값을 알아야 하기 때문에 RNN이 효과적이게 된다.

- RNN에 넣어야 할 입력데이터를 가공하는 것이 복잡하다.

### one-hot encoding

- h, i, e, l, o의 unique한 문자가 있다.

- vocab, voc문자열의 단어가 있다. 원핫인코딩의 사이즈가 된다.

- One-hot encoding을 vocab으로 쓸 수 있다. 인덱스를 one-hot으로 바꾸면 one-hot encoding이 되게 된다.

- 문자열을 원핫인코딩으로 바꾸는 과정, dictionary를 통해서 문자열을 숫자로 바꾸고, 숫자를 문자로 바꾸는 것을 자유롭게 하면 RNN을 자유롭게 쓸 수 있다.

- 입력의 값은 5개가 된다. sequence길이는 6개가 된다. 출력의 dimension hidden은 5개가 된다.(i,h,e,l,l,o)

- batch는 1이 된다.

# Creating rnn cell

- cell의 사이즈를 정하는 것이 중요하다.

- rnn_size가 5라면 입력의 사이즈를 정할 수 있다.

- X와 Y를 placeholder로 정의할 수 있다. 마지막 hidden_size, input_dim이 된다. sequence_length가 one_hot의 길이를 결정한다.

# Sequence_loss

- sequence를 받아들인다. logits(예측)을 입력받고, target true데이터를 받는다. weight는 각각의 자리를 중요하게 생각하는지를 받는다.

- one_hot의 형태로 줬다면, 예측값이 얼마나 틀렸을지 정하는 것이 Loss이다.

