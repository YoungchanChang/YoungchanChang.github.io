---
layout: post
title: 파이썬 장고 회원정보 수정 
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[URL REVERSE](https://wayhome25.github.io/django/2017/05/05/django-url-reverse/)

# 기본 로직

<center>
<figure>
<img src="https://imgur.com/qYcME8Y.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

# READ작업하기

- DB에서 유저의 정보를 반환할 때 아래와 같은 코드를 쓸 수 있다. user.get_absolute_url()를 클릭했을 때, user:profile링크로 **유저의 pk를 갖고** 가게 된다.

```python
    def get_absolute_url(self):
        return reverse("users:profile", kwargs={"pk": self.pk})
```

- get_absolute_url()을 설정하면 admin사이트에서 자세히 볼 수 있게 된다.

# 중요한 문제 - 다른 사람 정보가 나오는 경우

- 상단의 userProfile을 클릭했는데, 내 정보가 아닌 다른사람 정보가 나오는 경유가 존재한다.

- 이 경우는 뷰에서 user정보를 호출할 때 `user/model.py`를 이용했기 때문이다. 유저가 대체된다.

- 유저상세보기 DetailView를 볼 땐 변수의 이름을 따로 줘야한다. 이것이 `context_object_name`이다.

```python
class UserProfileView(DetailView):

    model = models.User
    context_object_name = "user_obj"
```

# 로직

<center>
<figure>
<img src="https://imgur.com/BTmJVln.png" alt="views">
<figcaption></figcaption>
</figure>
</center>

- 1.사용자 페이지에서 `<li class="nav_link"><a href="{{user.get_absolute_url}}">Profile</a></li>`로 사용자가 보기를 클릭한다.

- 2.user 모델 객체의 get_absolute_url메소드는, user:profile URL을 찾는다.

```python
def get_absolute_url(self):
    return reverse("users:profile", kwargs={"pk": self.pk})
```

- 3.users:profile은 URL에서 `path("<int:pk>/", views.UserProfileView.as_view(), name="profile")`를 타고 VIEW를 찾는다.

- 4.UserProfileView객체에 user모델의 p.k를 전달한다.

- 5.VIEW클래스에서 사용자의 데이터를 읽은 뒤 반환한다.

- detailview를 상속받으면 자동으로 user_detail.html에 렌더링을 한다. 여기에서 변수의 이름을 "user_obj"로 하면 p.k가 user_obj를 찾는다. 반면 여기에서 변수의 이름을 주지 않으면 user변수 이름으로 찾는다.

```python
class UserProfileView(DetailView):
    model = models.User
    context_object_name = "user_obj"
```

- 6.view객체가 렌더링을 해서 사용자에게 보여준다.

### 프로필 변경 클릭시 아래 링크를 타고 간다.

- `<li class="nav_link"><a href="{{user.get_absolute_url}}">Profile</a></li>`

- OR `<li class="nav_link"><a href="{% url "users:logout" %}">Log out</a></li>`

- 여기서 유저 변수를 기억하는 것은 로그인 했을 시 user변수 이름으로 기억하게 만들었기때문이다.

- 유저가 로그인 화면에서 로그인 시 -> user변수로 관리하게 된다.

```python
    user = authenticate(self.request, username=email, password=password)
    if user is not None:
        # user변수로 유저들을 관리하게 된다.
        login(self.request, user)
    return super().form_valid(form)
```

### 사용자가 방 상세보기에서 유저 프로필 보기를 클릭했을 때

- 방 상세보기 페이지의 링크는 아래와 같다.

- `<h2>By: <a href="{{room.host.get_absolute_url}}">{{room.host.username}}</a>` user의 p.k번호를 전달한다.

- `path("<int:pk>/", views.UserProfileView.as_view(), name="profile"),`

- 해당 p.k를 바탕으로 view를 찾는다.

- `context_object_name = "user_obj"`설정을 안하면 Profile을 클릭했을 때, user로 찾게 된다. 그러면 덮어씌워지게 된다.

- HTML에서 파일이름이 읽어질 변수를 정해라.

- DetailView를 가져올 때 user_detail.html을 자동으로 찾는다. 여기에서 context로 줄 변수는

- models.User에서 받은 p.k을 찾는다. 여기서 view에다가 던져줄 값의 이름은 user_obj로 한다. 이걸로 안 하면 user로 덮어씌워지게 되고 **Profile까지 영향**을 준다.

```python
class UserProfileView(DetailView):

    model = models.User
    context_object_name = "user_obj"
```

### 고고고고 여기다!!!!!!!!!!

- **생략된 개념**

- ListView를 상속받으면, as_veiw()메소드를 썼을 때, 자동으로 room_list.html을 찾는다.

- 해당 모델에 매칭되는 변수 이름을 가져다 쓴다.

- 그래서 덮어씌워진다.