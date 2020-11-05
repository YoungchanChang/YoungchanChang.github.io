---
layout: post
title: 파이썬 장고 Message 
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[메시지 프레임워크](https://docs.djangoproject.com/en/3.1/ref/contrib/messages/)

# 메시지 프레임워크

- 장고의 메시지는 **flash message**기능이다. flash message는 서버에서 사용자의 form처리나 사용자의 input을 사용자에게 보내주는 처리를 할 때 쓰인다.

- 장고는 익명이나 인증된 사용자에게 쿠키와 세션을 사용해서 메시지를 제공한다. 메시지 프레임워크는 요청에 대해 **잠시 메시지를 저장**할 수 있게 해준다. 모든 메시지는 **중요도를 가리키는 태그**를 갖는다.

### 메시지 프레임워크 사용

- 장고의 메시지 프레임워크는 middleware로써 settings.py의 INSTALLED_APPS에서 볼 수 있다.

- 메시지의 저장은 session에 의존하기 때문에 SessionMiddleware는 MessageMiddleware보다 먼저 활성화되어야 한다.

### Context

- 장고는 뷰에서 **템플릿에 데이터를 전달**하기 위해 context를 쓴다. 장고에서는 RequestContext를 쓴다. RequestContext는 기존 Context와 다르게 **첫번째 인자로 request**를 쓴다. 또한, context_processor를 사용해서 컨텍스트에 **변수를 추가**한다.

- context_processor는 `request object`를 인자로 받은 뒤에 context에 dictionary로 통합시킨다.

- `django.contrib.messages.context_processors.messages'`를 사용하기 때문에 **템플릿에서 messages변수 안**에 메시지 내용을 담을 수 있게 된다. message변수 안에 멤버변수들 (messages.error에서 error)의 경우 태그안에 class 변수로 쓰일 수 있다.

### 실제 활용

- 사용자가 값을 잘못 입력했을 때, 서버에서는 예외로 처리하면서 사용자에게 잘못된 값을 전달했다고 사용자에 notify할 수 있다.

 메시지는 **refresh하면 없어지며**, 오직 한 번만 보여준다. `one-time notification`을 보낼 수 있다.

```python
def kakao_callback(request):
    try:
        code = request.GET.get("code")
        # 사용자 요청에 대해서 GET.code("code")로 분석한 뒤에 예외처리를 진행한다.
        raise KakaoException()
        
        return redirect(reverse("core:home"))
    except KakaoException:
        # 예외 발생 시에 오류 메시지를 띄운다. 메시지 변수는 proprecssor에 의해서 템플릿에서 쓸 수 있게 해준다.
        messages.error(request, "Something went wrong")
        return redirect(reverse("users:login"))
```

### 예외 클래스 만들기

- KAKAOEXCEPTION 클래스를 만들 수 있다.

- if else대신에 if raise로 예외처리를 한 다음에 exeception에서 받으면 훨씬 더 깔끔하다!!!

```python
        if error is not None:
            raise KakaoException("Can't get authorization code.")
```

### 스타일링

- absolute div와 inset의 차이는

- `Use .absolute to position an element outside of the normal flow of the document,`

# 추가로 알아 두면 좋은 정보

## fixed와 absolute의 차이

- 헤더는 fixed이지만 웰컴은 absolute인 이유는 스크롤했을 때 메시지가 따라올 필요가 없기 때문

[참고](https://zetawiki.com/wiki/CSS_position_absolute,_fixed_^EC^B0^A8^EC^9D^B4_^EC^83^81^EC^84^B8)



### message engine

- [참고](https://docs.djangoproject.com/en/3.1/ref/contrib/messages/#message-storage-backends)

- 메시지 프레임워크는 임시 메시지를 저장하기 위해 다양한 백엔드를 사용한다.

- `django.contrib.messages`안에 3가지 클래스를 사용한다.

- storage.session.SessionStorage : request's session에 대한 모든 메시지를 저장한다.

- storage.cookie.CookieStorage : 요청에 대한 알림의 지속성을 위해 쓰인다. 쿠키의 2048bytes를 넘어가면 오래된 메시지들은 폐기된다.

- storage.fallback.FallbackStorage : 기본 클래스. 먼저 CookieStorage를 쓰고 single cookie에 맞지 않는 경우 SessionStorage를 쓴다. contrib.sessions 앱을 필요로한다.

- 나만의 저장 class를 만들고 싶다면, BaseStorage클래스를 상속받으면 된다.
