---
layout: post
title: 파이썬 장고 DetailView
category: Django
tags: [python, Django]
comments: Django
---

- 방의 목록을 클릭했을 때 세부정보가 나와야 한다. 방의 목록을 클릭하면 해당 방의 고유값인 p.k를 전달한다.

- p.k를 바탕으로 방의 정보를 불러와서 렌더링한다.

# URL설정하기

- 먼저 config파일 `path("rooms/", include("rooms.urls", namespace="rooms")),`에서 경로를 설정한다.

- room.urls파일에 app_name을 설정한다. 그리고 urlpatterns를 설정한다. `urlpatterns = [path("<int:pk>", views.room_detail, name="detail")]` 장고는 room_detail이라는 함수를 호출할 때,  

# 기존 URL경로의 문제점

- 방을 상세보기를 클릭하려면, 리스트에서 p.k값을 넘겨줘야한다. 그런데 경로를 "/rooms/{{room.pk}}"이런 식으로 구성하게 되면, 매번 경로를 재설정해줘야한다.

- namespace는 /rooms/1/edit-room을 기억하지 않는다. namespace와 name을 쓰는 방법?

- url에서는 app_names와 namespace를 붙였다. config에서 include로 해당 경로를 불러낼 때 namespace를 전달해준다. 그리고 urls.py에서 name으로 해당 경로의 명칭을 지정해준다.

```
{% for room in rooms %}
<h3>
    <a href="/rooms/{{room.pk}}">
        {{room.name}} / ${{room.price}}
    </a>
</h3>
<h1>{{room.name}}</h1>
{% endfor %}
```

- **따로 url을 하나하나 구성하지 않아도 된다.** namespace:경로 argument

```
    <a href="{% url "rooms:detail " room.pk%}">
        {{room.name}} / ${{room.price}}
    </a>
```

### get_absolute_url

- 웹 사이트에는 어떻게 보이는지 컨트롤한다. `1/rooms/121로 가거나 rooms/171`로 간다.

- `def get_absolute_url(self): return "/potato"`를 만들면 우측 상단에 VIEW ON SITE가 뜨고 내가 어떤 url을 갖고 있던 간에 그곳으로 이동시켜 준다.

- url에 namespace와 name으로 접근한다.

- reverse는 url name을 필요로하는 function이다. 그리고 해당 url을  return한다.

- **reverse를** 최대한 많이 쓰자. url보다 도움이 된다.

- raise 404를 올리지 않으면 정보가 없는 거랑 다르다.

### get_absolute_url()

- get_absolute_url()dms URL을 위한 객체를 설정해준다. reverse()함수를 쓰면 훨씬 편하다.

- get_absolute_url()는 관리자 페이지에서 주로 쓰인다. 해당 메소드를 설정하면 "View on site"링크가 뜨게 된다.

### reverse()

- url템플릿 태그를 내 코드에서 쓰고싶을 때 상요하는 메소드이다.

- kwargs와 args는 동시에 같이 들어갈 수 없다.  매칭되는 것이 없다면 NoReverseMatch exception 예외를 발생시킨다.

```python
from django.urls import reverse

def myview(request):
    return HttpResponseRedirect(reverse('arch-summary', args=[1945]))

OR

>>> reverse('admin:app_list', kwargs={'app_label': 'auth'})
```

# Http404()

- 브라우저가 404 status를 이해할 수 있기 때문에 쓸 수 있다. 그냥 404페이지를 보여줘도 된다. 

- redirect URL을 직접 만드는 것 보다 그냥 raise하면 편하다. redirect를 할 필요 없고 다른 url을 만들 필요도 없다.

- 페이지를 찾을 수 없을 때 HTTP헤더에 제공하는 메서드이다. 

- 아래와 같이 redirect로 처리할 수도 있지만, 

```python
    except EmptyPage:
        return redirect("/")
```

- 아래와 같이 redirect할 수도 있다. Http404()에러를 발생시킬 수 있다.

```python
    except models.Room.DoesNotExist:
        return redirect(reverse("core:home"))
        raise Http404()
```

### DetailView()

- DetailView()도 클래스로 만들 수 있다. ListView와 다른 차이점은 페이지가 아니라 p.k가 필요하다는 점이다.

- http 404 에러를 보내지 않았어도 자동으로 가게 된다.

- 코드가 많을 수록 무엇이 일어나는지 알기 쉬워진다.

# 참고

[url dispatcher](https://docs.djangoproject.com/en/2.2/topics/http/urls/)

[get_absolute_url](https://docs.djangoproject.com/en/3.1/ref/models/instances/#django.db.models.Model.get_absolute_url)

[reverse](https://docs.djangoproject.com/en/2.2/ref/urlresolvers/#django.urls.reverse)