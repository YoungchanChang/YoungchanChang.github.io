---
layout: post
title: 리눅스
category: linux
tags: [linux]
comments: linux
---

# 에러코드

- 에러 내용 : python socket.error: [Errno 98] Address already in use [closed]

- 원인 : 이미 소켓이 사용중임

- 해결책 : `$ lsof -i :8000`로 사용중인 소켓 확인. kill -옵션 PID로 해당 프로세스 종료 후 재시작

# 참고

[소켓 확인](https://stackoverflow.com/questions/17780291/python-socket-error-errno-98-address-already-in-use)

[프로세스 킬](https://121202.tistory.com/45)