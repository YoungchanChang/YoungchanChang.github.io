---
layout: post
title: 파이썬 장고 sizes 
category: Django
tags: [python, Django]
comments: Django
---

# sizes다루기

- em은 `가장 가까운 font-size`와 같다.

- rem은 `root element size / root은 html의 font-size`와 같다.

- 단위가 font-size에 비례한다는 것에 장점이 있다.

# Header

- container은 기본 layout이다. max-width를 설정할 때 사용한다. 스크린 사이즈를 정해놓고 작업할 때 유리하다.

- `<div class="container mx-auto">` 태그를 쓰면 가운데 정렬을 할 수 있다.

- `.max-w-full`클래스와 함께 쓰면 max-width를 컨트롤할 수 있다.

- 가로길이는 width로 정한다. `w-8`로 적으면 된다.

### flex

- flex는 안의 속성을 늘어나거나 줄어들게 해준다. grow and shrink

- flex를 쓰면 컬럼을 세로로 정렬해준다.

- Align Items - `flex와 grid안의 아이템들이 컨테이너 축에 어떻게 두느냐르 ㄹ결정`

- 

- flex안의 속성으로 item이 있다. items-center을 쓰면가운데로 온다.

# shadow

- effects로

- hover도 추가할 수 있다. 마우스가 올라갈때 변화하는 방식이다.

- focuse도 추가할 수 있다. focus:outline-none

- transition은 클래스 안에 속성을 주면 된다.

- 사이즈를 width로 조절할 수 있다. 부모 사이즈에 비례한다.

# 상단에 헤더 고정하기

- fixed 속성을 이용하면 된다. 사이의 간격은 margin으로 한다.

- inset-0를 이용하면 절대값으로 위치된다.