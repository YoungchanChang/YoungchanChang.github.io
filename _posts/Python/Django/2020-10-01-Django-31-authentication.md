---
layout: post
title: 파이썬 장고 LOGIN & LOGOUT
category: Django
tags: [python, Django]
comments: Django
---

# CSRF란

- 장고에서 username은 매우 중요하다. username을 email인 것처럼 사용해서 app을 만들 수 있다.

- username을 체크하고 email도 체크하는 중복체크를 하지 않기 위해서이다.

- CSRF는 Cross Site Request Forgery.

- 웹사이트에서 로그인할 때, Cookie를 준다.

- 페이스북이 나에게 쿠리를 주면 나는 쿠키를 페이스북에 보낸다. 내가 페이스북이 아닌 다른 웹사이트를 방문했을 때, 페이스북에 뭔가를 요청할 수 있다. 나의 브라우저에서 자동으로 쿠키를 보내면, 다른 웹사이트에서 페이스북 백엔드로 보내게 된다.

- 내가 버튼을 클릭할 때 사람들은 나의 비밀번호를 바꿀 방법을 알아낸다. 다른 웹사이트에서 페이스북으로 form을 보내게 된다.

- 장고에서는 csrf_token을 사용하나.

- token은 만약 다른 사람이 다른 웹사이트에서 post request를 보낸 것을 찾았더라도 토큰을 갖고 있지 않는다.

- 토큰은 기본적으로 post request가 이 웹사이트에서 왔느지 확인한다.

### Validating Email and PAssword

- 만약에 이메일이나 비밀번호가 있는 field를 확인하고 싶으면 **method의 이름은 clean_이어야 한다.**

- 메소드의 이름은 clean이여야 한다.

- `if form.is_valid(): print(form.cleaned_data)`에서 cleaned_data는     `def clean_pasword(self): print("clean password")`의 결과물이다.

# Login Logout

- 사용자가 한 번 로그인 사이트는 어느 페이지를 가더라도 사용자 정보가 유지되어야 한다.

- HTTP통신은 단발성 통신이기 때문에, 사용자 정보가 유지될 수 없다.

- 사용자 정보 입력 (request) -> 정보가 DB에 저장되어있는지 인증 -> 맞다면 쿠키, 세션 제공 -> 

- 1.clean메소드로 id, pw 검증 오로지 예외처리!!!!!!!!/

- 2.실제로 인증, USER객체 반환

- 3.세션값 제공(login메소드를 쓰며, httprequest와 user객체를 쓴다. userid를 session값으로 쓴다. == 같은 id면 같은 session)

- 장고가 **쿠키도 반환**해준다!!!

- authentication은 username을 필요로한다.

```python
from django.contrib.auth import authenticate
user = authenticate(username='john', password='secret')
```

- 장고에는 ContextProcessor가 있다. context_processor은 함수인데, 나의template에 정보를 추가하는 일을 한다.

- user의 contextProcessor은 cookie를 가져와서 user를 찾고 template에 자동으로 넣어준다.

- 쿠키를 가지고 와서 user를 찾고 template에 자동으로 넣어준다.


# Login View를 사용하자

- 문제는 LoginView는 email이 아니라 username을 요구한다는 것이다.

- username과 password를 사용하지 않으면 된다.

- PasswordResetForm은 EMAIL도 보내준다.

- FormView는 template_name

- FormView의 장점은 훨씬 깔끔해진다는 것이다!!!

# 참고

[CSRF](https://docs.djangoproject.com/en/2.2/ref/csrf/)

[Authentication](https://docs.djangoproject.com/en/3.1/topics/auth/default/)

[login_logout](https://docs.djangoproject.com/en/3.1/topics/auth/default/)

[Context_Proprecssors](https://docs.djangoproject.com/en/3.1/ref/templates/api/#playing-with-context-objects)

[LoginView, AuthenticationForm](https://docs.djangoproject.com/en/3.1/topics/auth/default/#django.contrib.auth.forms.AuthenticationForm)