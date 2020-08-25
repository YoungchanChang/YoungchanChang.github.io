---
layout: post
title: React props state event 정리
category: React
tags: [react, event]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24860)를 정리한 글입니다.  
> 헷갈리는 개념은 이미지 검색하면 좋은 인포그래픽이 많다.

# 헷갈리는 개념은 이미지 검색하면 좋은 인포그래픽이 많다.

- props는 오직 읽기 전용입니다. props의 값은 컴포넌트를 사용하는 쪽에서만 줄 수 있습니다.

<center>
<figure>
<img src="https://imgur.com/8FQHs8Q.png" alt="views">
<figcaption>props는 읽기 전용으로 컴포넌트 내부에서 값을 바꿀 수 없다.</figcaption>
</figure>
</center>

- 반면 state는 내부 데이터를 다룹니다. 

<center>
<figure>
<img src="https://imgur.com/q6yGOkF.png" alt="views">
<figcaption>state는 컴포넌트의 내부 데이터를 다룬다.</figcaption>
</figure>
</center>

- 상위 컴포넌트에서 하위 컴포넌트의 데이터를 바꿀 때는 props를 쓰고, 하위 컴포넌트에서 상위 컴포넌트의 데이터를 바꿀 때는 event로 상위 컴포넌트의 state값을 호출합니다.

<center>
<figure>
<img src="https://imgur.com/VMfxkxq.png" alt="views">
<figcaption>state는 컴포넌트의 내부 데이터를 다룬다.</figcaption>
</figure>
</center>
