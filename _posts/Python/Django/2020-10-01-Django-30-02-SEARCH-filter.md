---
layout: post
title: 파이썬 장고 SEARCHVIEW
category: Django
tags: [python, Django]
comments: Django
---

# 내가 원하는대로 필터링하기

- Field lookup기능이 있다. F.K로 연결된 db를 가져올때는 set을 쓰고, 데이터를 필터링하기 위해서는 `__ 2개의 언더라인`을 쓴다.

- 만약에 언더라인 두개가 없다면 편의상 exact로 간주한다.

```python
Entry.objects.get(id=14)
```

### 필터링

- **필터링의 여러 조건들을 딕셔너리 객체에 넣은 다음에 unpacking할 수 있다.**

- `test = models.Room.objects.filter(amenities__pk=14)`Room객체는 amenities를 ManytoMany로 선언했다. foreingkey__pk를 통해서 해당 데이터를 가져올 수 있게 된다.

- `test = models.Amenity.objects.filter(rooms__id=49)`를 통해서 접근이 가능함.

- `test = models.Amenity.objects.filter(rooms__country="CV")`를 통해서도 접근이 가능함. 접근이 가능한 이유는 Room에서 선언해줬기 때문

```python
        filter_args["room_type__pk"] = room_type
 
    # Room 에서 room_type은 선언해서 접근 가능
    # room_type에서 역으로 room접근은 어떻게함? room_type(pk=1)한 다음에 rooms.로 가져오면 됨

        test = models.Amenity.objects.filter(rooms__country="CV")
```

- oneToMany에서 one에서 Many를 선언한다. 선언한 곳은 변수명을 통해 접근할 수 있고, 선언당한 쪽은 related_name을 통해 접근이 가능하다. >>> a.room_set.all()

- ManyToMany는 

- 원하는대로 어떤 수보다 크거나, 작거나, 단어로 시작하는대로 필터링할 수 있다.

- 원하는 손님 수보다 같거나, 많은 방들의 정보를 돌려보내줘야 한다.

- 필터링과 조건부 필터링을 이용할 수 있다.

# Forms API

- HTML태그를 빨리 만듬. 2 데이터를 다 정리해서 줌. string을 integer인지 확인해줌

- 장고Form을 쓰는 이유 : 기존 폼은 DB에서 데이터 불러와서 해당 데이터를 html로 render했다.

- html에서는 템플릿처럼 label, value, placeholder, selected를 만들었어야한다.

- 만약 장고 Form을 쓴다면 **label, value같은 태그들을 안 써도** 된다. html의 긴 태그들이 [[form}} form객체 안에 들어가게 된다.

- OneToMany와 관련된 필드 - ModelChoiceField / ManyToMany와 관련된 필드 - ModelMultipleChoiceField

- 단 querysetr은 넘겨줘야한다.

- 기존 모델의 엵과 맞춘다.

- 옵션으로 empty_label을 줄 수 있고, 해당값이 빈값이어도 된다면 required=True로 한다.

- form태그를 쓰는 장점? 데이터를 정리해서 준다. 무언가 없게끔 확인해주고, 

### form태그에서 GET받기

- form에서 SearchForm을 받는 방법. `form = forms.SearchForm(request.GET)`로 GET으로 받을 수 있다.

- 그러면 form이 어디에 체크되어있는지 알고있다.

- form은 자동으로 에러를 기록한다.

- unbound form은 form안에 데이터가 없는 상태이다. 여기에서 데이터를 넣으면 bounded form이 된다. 자동으로 데이터를 인증해준다.

- 비어있는 GET을 준다면 에러를 발생!!!!!!!!!!!!!!!!!!! 아래와 같이 GET데이터를 하나 가져온다.

```python
    country = request.GET.get("country")

    if country:

        form = forms.SearchForm(request.GET)
```

- cleaned_data는

# 반드시 알아야  할 사항

- ctrl+p를 눌러서 파라미터를 보거나 ctrl+q로 해당 설명을 보는 것이 도움이 된다.

# 참고

[multi-valued realtion](https://docs.djangoproject.com/en/2.2/topics/db/queries/)


[querysets](https://docs.djangoproject.com/en/2.2/ref/models/querysets/)


[Forms api](https://docs.djangoproject.com/en/2.2/ref/forms/api/)

[Form Field](https://docs.djangoproject.com/en/2.2/ref/forms/fields/#required)

[인자값 확인하기](https://gmlwjd9405.github.io/2019/05/21/intellij-shortkey.html)