---
layout: post
title: flask에서 엘라스틱서치 검색유사도
category: python
tags: [python, 쓰기]
comments: true
---

# BM25의 원리

- BM25의 점수 방식 : `score(freq=1.0), computed as boost * idf * tf from:`

- idf에 tf를 곱한 뒤에 boost를 곱한다.

<center>
<figure>
<img src="https://imgur.com/4CqjBHk.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### IDF계산방식

- idf의 점수 `idf, computed as log(1 + (N - n + 0.5) / (n + 0.5)) from:`

<center>
<figure>
<img src="https://imgur.com/AJXr6GY.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

  - N은 **document 전체의 수**이고 n은 해당 token을 **포함하고 있는 document의 수**이다.
  
  - 해당 token을 포함하고 있는 document수가 높으면 높을 수록 점수는 낮게 나온다. 101개의 문서중에 오직 1개만 해당 단어를 포함하고 있다면 해당 score은 1.826 로 나온다. log(1 + (101 - 1 + 0.5) / (1 + 0.5))

### TF의 계산방식

  - tf의 점수 `tf, computed as freq / (freq + k1 * (1 - b + b * dl / avgdl)) from:` 
  
  - dl은 document length(문서의 길이)로 **해당 document의 length**이다. avgdl은 average length of field이다. **해당 field는 모두 같은 값**을 갖게 된다. 전체 문서의 평균과 한 문서의 길이라는 점을 명심하자!
  
  - 단어가 포함된 field에서 짧은면서 많은 단어를 포함하면 높은 점수를 받는다.

  - b가 0이라면 문서의 길이를 고려하지 않겠다는 의미가 도니다. b가 1이 될 수록 문서의 길이에 많은 가중치를 두어서 계산한다는 뜻이 된다.

  - k1이 0이라면 모든 텀은 다 지워지고 위의 식이 1이 된다. tfㅇ

# 요약

1. 내가 날린 query 안의 term이 적은 문서에만 있는, 즉 매우 희소하고 자주 쓰이지 않는 단어여야 하며,

2. 문서에서 해당 term이 많이 나와야 하며,

3. 해당 문서의 길이는 짧아야 한다.



# 테스트

- 아래 예시에서 the horse로 검색했을 때 doc2가 먼저 나온다. the가 2번 들어간 "the horse and the mouse"가 출력될 수 있지만, **문서의 길이가 더 김**으로 doc2가 출력된다.

```
doc1
"text": "The horse and the mouse",

doc2
"text": "The horse",
```

### 테스트02

- 문서의 영향력 줄이고, tf의 영향력 늘리기

- 쇼핑몰같은 경우 많은 검색에 노출되고 싶어서 단어를 여러번 반복한다. 상황에 따라서 tf의 영향력을 늘려야 하는 경우만 늘린다.

```
doc1
"text": "The horse and the mouse",
"tip": "grass horse",


```

# OR나 AND일 경우 어떻게 점수가 계산됨? 중복됨?

# 참조

[위키피디아 BM25](https://en.wikipedia.org/wiki/Okapi_BM25)

[용어들 요약해 놓은 글](https://jitwo.tistory.com/8)

[BM25 파마리터](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules-similarity.html)

[discount-overlaps](https://stackoverflow.com/questions/44115497/elasticsearch-similarity-discount-overlaps)

[좋은 자료](https://littlefoxdiary.tistory.com/12)