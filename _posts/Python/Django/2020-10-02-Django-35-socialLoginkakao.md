---
layout: post
title: 파이썬 장고 LOG IN WITH KAKAO
category: Django
tags: [python, Django]
comments: Django
---

# 카카오 로그인

- 카카오로그인은 github와 유사하다.

- 다만, 받아오는 값이 무엇인지 알아야 된다. 이메일이 안 올수 있다.

- 이메일이 안 오면 사용자를 저장하지 않고 오류를 처리하면 된다.

# 이미지 넣는 방법 - 이미지 다운받아서 보기

- 카카오 이미지를 다운받은 뒤에, 거기다 넣어준다.

- profile_image가 없다면, photo를 requests해서 가져온다.

- user의 아바타 필드(ImageField)에는 FileField에는 save메소드가 있다. 

- user의 avatar에 save를 둔다. **두번째 파라미터**를 이해하는 것이 중요하다.

- image를 request하기 때문에, photo_request.context()는 0과 1로 이루어지게 만든다.

- 1.URL로부터 이미지를 받아온다. 2. 파일을 IMPORT한다면, Raw파일로 처리한다.

- .content()는 0과 1로 만들어진 파일로 처리한다. 파일의 표현과는 상관이 없게 한다.

- Content는 raw content를 가진 파일이다. 파일로 만들어지게 된다.

# 이미지 처리 방법

- profile image url을 넣어주고 처리하는 방법도 있다.


# 내장된 폼

- built-in forms

- UserCreationForm

- form을 확장할 수도 있다.

- 오버라이딩해서 쓸수도 있다.

- 실제 코드를 보면 매우 비슷하다!!!!!!!!! 단, 이미 저장되어있는 기능을 이용할 수 있다.

- UserCreationForm을 사용하지 않더라도, 내부 코드를 참조하면 좋다.

- 내부 코드 또한 validate_password를 이용한다.

# 참고
[OAuth](https://docs.github.com/en/free-pro-team@latest/developers/apps/authorizing-oauth-apps)

[OAuth](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/)
