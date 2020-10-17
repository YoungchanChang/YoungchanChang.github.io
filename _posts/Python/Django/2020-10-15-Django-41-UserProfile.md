---
layout: post
title: 파이썬 장고 회원정보 수정 
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[URL REVERSE](https://wayhome25.github.io/django/2017/05/05/django-url-reverse/)

[메시지 프레임워크](https://docs.djangoproject.com/en/3.1/ref/contrib/messages/)

# 메시지 프레임워크

- pk값을 주는 이유?

- {{user.get_absolute_url을 쓸 수도 있다. 만약 adminpanel로 가서 카카오 쥬러를 클릭하면 view on site가 있다.

- 웹사이트에서 자세히 보고 싶으면 get_absolute_url은 요긴하게 사용될 수 있다.

###

- url "users:profile" 이랑 pk라고만 할 수도 있다. users.pk라고 할 수 없다. 

- admin패널에서 VIEW버튼을 쓰기 위해서  profile에서는 pk만 전달하지 않는다. get_absolute_url을 쓰면 된다.

```python
    def get_absolute_url(self):
        return reverse("users:profile", kwargs={"pk": self.pk})
```

#### 중요한 문제

- UserProfileView에서는 user값들을 바꿔버리고 있다.

- 메인 뷰에서는 로그인 한 사람이다.

- 방에서 사용자 정보를 본 뒤에 Profile을 누르면 내 정보가 아니라 사용자 Profile이 나오게 된다.

- 유저가 대체 된다.

- DetailView에서 SingloeObjectMixin을 보면 `context_object_name`가 있다. 로그인 했던 유저가 아니라, 뷰에서 찾았던 유저 객체를 가리키는 방법을 바꿀 수 있도록 해준다.

- 뷰를 작업할 때 만들어야 하는 가장 중요한 점이다

- UserProfileView가 뷰에서 찾았던 유저에 의해서 유저를 대체한다.

###

- DetailView가 하는 역할을 더 자세히 알아야 할 것 같다!!!

- context_object_name 객체의 역할 `Designates the name of the variable to use in the context.`

- 유저 상세보기를 클릭하면 아래의 링크를 타고 간다.  UserProfileView에서는 p.k아이디값을 변수로 받게 된다.

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