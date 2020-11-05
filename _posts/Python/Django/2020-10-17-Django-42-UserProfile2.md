---
layout: post
title: 파이썬 장고 회원정보 수정 
category: Django
tags: [python, Django]
comments: Django
---

### context란?

- context? 문맥. 글을 읽는 흐름. **앞 뒤에 데이터**가 있어야 한다. html의 경우에는 앞 html과 뒤 html이 존재한다.

###

[get_context_data](https://docs.djangoproject.com/en/3.1/topics/class-based-views/generic-display/)

- 하나 힘든 것은 context_data는 뭐니?

- python FBV에서 메소드는 아래와 같다. context에서 결정된다.

```python
def render(request, template_name, context=None, content_type=None, status=None, using=None):
    """
    Return a HttpResponse whose content is filled with the result of calling
    django.template.loader.render_to_string() with the passed arguments.
    """
    content = loader.render_to_string(template_name, context, request, using=using)
    return HttpResponse(content, content_type, status)
```

- CBV에서도 context를 이용할 수 있다.

- `get_context_data`로 DB에서 가져온 데이터를 뷰(문맥)에 맞춰서 전달할 수 있따!!!!!!!!!!

- CBV를 활용해서 user에 profile, bio추가하기


### Profile 고려사항

- 아바타가 있을 때와 없을 때. 없을 때는 대문자만 보여지게 한다.

- 추가로 해야될 부분 first name filtering

- 꿀팁 `flex jusify-center items-center` 안에 들어있는 item을 가운데 정렬한다.

- overflow-hidden은 뭘까?

- UserUpdate를 하면 자동으로 `get_absolute_url()`로 간다.

### UpdateView

- UpdateView가 없다면 request하고 다시 read한 것을 form에 대입해야한다.

- form_valid()의 타당성도 고려해야한다. 

- 템플릿 랜더링 기능, form안에 데이터 넣기, form 검증하기 기능이 있다.

- but control이 떨어진다. custom하기 힘들다.

- **Form클래스를 사용해서 custom**할 수 있다.!!!!!!!!!!!!!!!!

- ViewClass의 장점을 극대화하기~!


### 사용자 경로 보호하기

- user_password_change로 들어가기만 해도 바뀐다 .이런 것들을 보호해야한다!!!!!!!!!!!!!!!!!!!

- 이게 궁금했던것!!!

- `Mixin은 추가적인 기능`을 제공한다.

- 뷰의 미들웨어 같은 것이다. 사용자에게 Mixin으로 보여주지 않게 한다....

- 오호라~!

- password로 로그인 하지 않았다면(카카오나 깃허브로 로그인) 사용자들이 URL경로를 알아도 접근 x해야한다.

- test_func()는 access_mixin에서 오게 된다. access_mixin에는 permission_denied등이 있다.


- success_url을 새로 설정할 수도 있다.

### Mixin

- **Middleware**같은 것이다. 하나하나나 검증을 거친 뒤에 값을 반환한다.

# 참고
Adding messages in class-based views
[success_message_mixin](https://docs.djangoproject.com/en/3.1/ref/contrib/messages/)

조건부 mixin
[UserPassesTestMixin](https://docs.djangoproject.com/en/3.1/topics/auth/default/)