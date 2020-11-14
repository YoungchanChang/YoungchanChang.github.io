---
layout: post
title: 파이썬 장고 LOG IN WITH GITHUB
category: Django
tags: [python, Django]
comments: Django
---

# OAuth의 작동 원리

- 소셜로그인 가입시 고려할 사항

- 사용자는 소셜로그인을 했으면 인증을 안 해도 된다.

- 이메일로 가입을 했다면 이메일 인증을 보낸다.

- 소셜로그인을 했다면 필수정보만 갖지 않게 될 수 있다. 따라서 **기본값 처리**를 해야한다.

- 사용자가 받은 code를 이용해서 웹에서는 접근을 한다. **code의 유효기간 처리를 해야한다.**

- 깃허브는 사용자가 웹사이트를 이용하겠다는 정보를 갖고 있으므로 signup이 필요 없이 바로 callback을 보내게 된다.

- 사용자는 깃허브에 소셜로그인 요청시 code를 받아서 웹 서비스에 건네준다. 웹 서비스는 해당 code로 깃허브에 사용자 정보를 요청하는데, 해당  code가 깃허브로부터 받지 않은 잘못된 경우 **예외처리**를 해야한다.

- 사용자 정보가 이미 있는 경우 DB에서 사용자 정보를 불러와야한다.

# 유저가 이미 웹사이트에 가입한 경우 깃허브 가입 처리는 어떻게하지?

- TRY CATCH로 감싸면 장점이 잦은 raise를 하지 않아도 된다.

### 오 개꿀

- 유저의 값이 없는 경우 가입을 시켜야한다. **비밀번호자체를 무력화**시킨다.

- 유저의 값이 있는 경우 : 유저는 로그인 시도를 한다. github로 시도했는지 파악한다. 아니면 에러

# 참고
[OAuth](https://docs.github.com/en/free-pro-team@latest/developers/apps/authorizing-oauth-apps)

[OAuth](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/)
