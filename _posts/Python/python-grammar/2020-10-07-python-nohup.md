---
layout: post
title: kwargs
category: python
tags: [python, dictionary]
comments: true
---

# 플라스크 서버 구동시 유의사항

flask OSError: [Errno 99] Cannot assign requested address

- 해결책 : 0.0.0.0으로 줘야한다.

백그라운드로 실행시

- nohup 
. bin
프로세스 킬

```console
 netstat -ntlp | grep :80
```
- 리눅프 포트 확인
https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%ED%8F%AC%ED%8A%B8_%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94_%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4_%ED%99%95%EC%9D%B8

# 참조

[플라스크 서버 구동시](https://stackoverflow.com/questions/26280868/flask-cannot-assign-requested-address)

[백그라운드 작업](https://blkcoding.blogspot.com/2018/03/nohup.html)

[백그라운드 2](https://bongjacy.tistory.com/entry/%EB%B0%B1%EA%B7%B8%EB%9D%BC%EC%9A%B4%EB%93%9C%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

[netstat](https://m.blog.naver.com/PostView.nhn?blogId=pxkey&logNo=221276188823&proxyReferer=http:%2F%2F59.29.251.41%2F)

[리눅스 프로세스킬](https://121202.tistory.com/45)

[프로세스](https://ghostweb.tistory.com/778)




