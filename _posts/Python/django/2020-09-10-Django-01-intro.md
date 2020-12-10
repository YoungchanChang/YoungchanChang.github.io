---
layout: post
title: Django 01 - 장고 에어비엔비 소개
category: Django
tags: [python, Django]
comments: Django
---

# 에어비앤비

- 사용자들끼리 방을 빌려주고 예약하는 웹 어플리케이션

- 1.사용자들에 관한 것. 2.방에 관한것

# 흐름도

<center>
<figure>
<img src="https://imgur.com/iYiZMOF.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

### 사용자와 방의 관계

- 사용자들은 방을 올린다. 방을 올리는 사람은 호스트 한 명 뿐이다. (1사용자 - M방)

- 사용자들은 방을 예약한다. 방마다 어떤 사용자가 얼마나 예약됬는지가 나온다.

- 사용자들은 방에 대해 리뷰를 단다.

- 사용자들은 자신들이 좋아하는 방의 목록을 따로 관리한다. 사용자는 하나의 리스트를 갖고 있고, 리스트에는 여러개의 룸을 갖고 있다.

### 방의 옵션

- 방에는 (Photos, RoomType, Amenity, Facilities)의 옵션이 있다.

- 방에는 한개의 RoomType이 있다. 여러개의 Amenity, Facilitiy를 갖을 수 있다.

- 방을 올릴 때 여러 개의 사진을 올릴 수 있다. (1방 - M사진)

### 사용자와 사용자 대화창

- 하나의 방이 있고, 그 안에 여러명의 사용자들이 참여한다.

- 사용자가 방 안에서 대화를 보낸다.

### 사용자에 관한 것

- 회원가입, 소셜로그인, 사용자 정보 수정

- 서버에서 사용자 식별은 cookie, session을 이용한다.

### Entity-Relationship

<center>
<figure>
<img src="https://imgur.com/iYiZMOF.png" alt="views">
<figcaption></figcaption>
</figure>
</center>
