---
layout: post
title: 파이썬 장고 Verify EMAIL
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[이메일 보내기](https://docs.djangoproject.com/en/3.1/topics/email/)

# 이메일 인증

### 이메일인증시 고려할 사항들

- 어떤 메일서버를 쓸 것인가.(구글이나 네이버를 쓴다면 AWS서버를 사용할 시 스팸처리 될 수 있다.)

- 인증 코드를 어떻게 처리할 것인가. 인증코드가 일치하는 회원이 실제로 가입에 성공하게 한다. 인증코드를 만드는 방법은 python에서 uuid.uuidv4()나 메일값을 해쉬처리해서 해쉬된 값만 보내주는 방법이 있다.

- 템플릿을 이용해서 보내기. 메일을 보낼 때 단순히 코드만 보내지 않는다. html코드형식으로 보낸다.

- html메시지는 string이다. message는 string형식이다.

### message에 html을 넣기

- 

### 이메일 라이브러리

- 장고에는 이메일 인증을 위한 기능이 있다.

- 서버만을 이용해서 보내게 되면 스팸함으로 메일이 보내질 것이다.

- email_host, emmail_port 등이 필요하다. 내 자체 서버에서 하면 아무데서나 가게 된다.

- mailgun.com을 이용한다. 10,000개 이상일 때 돈을 낸다.

- 신용카드 없이 이메일을 만든다면 계정을 만든 이메일로만 보낼 수 있다. 신용카드 정보를 입력하면 아무한테나 이메일을 보낼 수 있다.

- 이메일이 작동하지 않으면 내 자신에게만 보낼 수 있다. 

- 장고 안에 있는 이메일 라이브러리를 쓰면 된다. 이메일 라이브러리에서는 몇 가지 설정을 해야한다. EMAIL_HOST, EMAI_PORT를 설정해야한다. EMAIL_HOST_USER과 EMAIL_HOST_PASSWORD를 설정해야한다.

- EMAIL_HOST는 이메일 서버에게 설정을 요청하는 것이다. 내가 만든 메일을 해당 서버에 요청하게 된다.

- EMAIL_USERNAME과 PASSWORD는 해당 서버에 들어가기 위한 ID,PW이다.

### django-env

- 깃허브에서 EMAIL_HOST_USER와 EMAIL_HOST_PASSWORD를 보면 안 됨으로, 새로운 환경을 설치한다.

- django-dotenv는 **.env파일을 read해서 이 모든 것들을 코드에 추가**한다.

- python의 최상위 폴더의 manage.py에 가서 dotenv를 import한다. 그리고 main()함수를 호출하기 전에 dotenv를 읽겠다고 선언한다.

- 이메일 인증 로직은 유저가 재사용할 수 있다.

- python에서 uuid.uuidv4()로하면 새로운 값을 뽑아낼 수 있다.

- 랜덤값으로 갖게 할 수 있다.

# 참고

[장고 이메일](https://docs.djangoproject.com/en/2.2/topics/email/)

[메일건](https://www.mailgun.com/)

[장고 dotenv](https://github.com/jpadilla/django-dotenv)