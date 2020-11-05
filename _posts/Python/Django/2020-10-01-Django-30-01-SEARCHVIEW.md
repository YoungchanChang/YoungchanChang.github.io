---
layout: post
title: 파이썬 장고 SEARCHVIEW
category: Django
tags: [python, Django]
comments: Django
---

# 검색기능

- view인데 검색이 가능하다. Searchbar는 언제나 상단에 있다. 그러니까 헤더에 안에 있으면 좋다.

- search 경로로 가서 처리하는 것이 좋다. "search/"를 쓰면 좋다.

- search는 form이 되어야 한다. search박스 안에서 검색어를 입력 => /room/search로 옮겨간다.

- input에는 name이 있어야한다!

- search경로에서는 해당 값을 포함해서 rendering한다. 

### SearchBar

- searchbar를 serach에서 안 보이게 하고, 다른데서 전부 보이게 하려면 헤더에다 아래와 같이 삽입한다.

- 무언가를 숨기게 하고 싶을 때 유용한 트릭이다.

```html
<header>

    [% include "partials/header.html" %]

    [% block search-bar %]
        <form method="get" action="{% url "rooms:search" %}">
            <input name"city" placeholder="Search by City" />
        </form>
    [% endblock search-bar %]
    
</header>
```

### Form

- 검색 결과가 그대로 떠있게 하기

- 헤더 안에 value를 그대로 둘 수 없다. search-bar만을 위한 block을 만든다.

- serachbar의 검색겨로가는 따로 관리하면 상단 위에 계속 떠있게 할 수 있다.

### 매우 유용한 트릭

- searchbar가 항상 상단에 떠있지만, 회원가입이나 로그인 시에는 searcbar가 없어져야한다.

- 이럴 때에는, search경로에서 해당 block을 없애면 된다.

- 언제쓰이나? 무언갈 숨기고 싶을 때

- 아닌 것만 block을 none처리한다. 로그인 페이지에서 nav bar이 보이지 않게 할 때 사용할 수 있다.

- 헤더를 특정 페이지에서 숨겨야 할 때 사용할 수 있다!!!

### 여러개의 데이터를 FORM에다가 보내기

- request에서 받는 모든 정보들은 전부 form으로 간다.

- DB에서 오는 것은 choices로 보낸다.


```python
    return render(
        request,
        "rooms/search.html",
        {**form, **choices},
    )
```

- 딕셔너리 객체 보내기. 보내야 할 데이터가 많으면, 관리하기가 불편하다. 딕셔너리 객체에 넣고 unpacking해서 보내면 편하다. unpacking하면 딕셔너리의 인자들이 차례로 들어가게 된다.

- 

```python
    choices = {
        "countries": countries,
        "room_types": room_types,
        "amenities": amenities,
        "facilities": facilities,
    }

    return render(request, "rooms/search.html", {**form, **choices})
```

- 리스트에서 오는 것은 아래와 같이 받을 수 있다.

- 같은 이름인데 다른 id값을 갖는 경우는 아래와 같이 list로 받을 수 있다.

- ex `amenities=7&amenities=14&facilities=2&facilities=3`

```python
    s_amenities = request.GET.getlist("amenities")
    s_facilities = request.GET.getlist("facilities")
```

- slufiy옵션은 모든 태그를 text로 변경시킨다. int와 string이 맞지 않을 때 발생하는 문제이다.

```html
    <input 
        id="f_{{facility.pk}}"
        name="facilities"
        type="checkbox"
        value={{facility.pk}}
        [% if facility.pk|slugify in s_facilities %]
            checked
        [% endif %]
    />
```

# filtering like a Boss

- Field lookup이 있다

- 원하는 손님 수보다 같거나, 많은 방들의 정보를 돌려보내줘야 한다.

- 필터링과 조건부 필터링을 이용할 수 있다.

# Forms API

- 장고가 알아서 label, value, placeholder, selected를 만들어 준다.

- form태그를 쓰는 장점? 데이터를 정리해서 준다. 무언가 없게끔 확인해주고, 

# 참고

[url dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/)


[kwargs](https://lee-seul.github.io/django/backend/2018/02/03/django-model-kwagrs.html)

[querysets](https://docs.djangoproject.com/en/2.2/ref/models/querysets/)

[unpack](https://wikidocs.net/22801)