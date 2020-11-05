---
layout: post
title: 장고 URL Reverse
category: webscraping
tags: [python, webscraping]
comments: python
---

# 참고

[Reverse](https://github.com/wayhome25/wayhome25.github.io/blob/master/_posts/Django/2017-05-05-django-url-reverse.md)

- 장고에서는 urls.py에서 **뷰에 대해** url변경을 하게 해준다.

# 장고 URL

- 기존에 url을 접근하려면 `https://comic.naver.com/webtoon/weekdayList.nhn?week=sat`와 같이 접근했다. 그런데 매번 `/webtoon/weekdayList.nhn?week=sat` 링크로 접근하기에 불편함이 있다.

- 장고에서는 이를 해결하기 위해 namespace와 name을 쓴다.

- 뷰에는 namespace나 name을 써서 접근할 수 있다.

- 아래와 같이 URL을 설정할 수 있다.

```python
urlpatterns = [ path("", include("core.urls", namespace="core")), ]
urlpatterns = [ path("login", views.LoginView.as_view(), name="login"), ]
```

# URL Reverse

- reverse함수는 urls.py에 선언해둔 **name에 따라서 url을 되돌려**보낸다. 

```python
from django.core.urlresolvers import reverse

reverse('blog:post_list') # '/blog/'
reverse('blog:post_detail', args=[10]) # '/blog/10/' args 인자로 리스트 지정 필요
reverse('blog:post_detail', kwargs={'id':10}) # '/blog/10/'
reverse('/hello/') # NoReverseMatch 오류 발생
```

- redirect함수는 특정 url로 이동하고자 할 때 사용한다.

```python
from django.shortcuts import redirect

redirect('blog:post_detail', 10)
# <HttpResponseRedirect status_code=302, "text/html; charset=utf-8", url="/blog/10/">
```

- reverse와 redirect함수를 쓰면 아래와 같이 쓸 수 있다.

```python
    return redirect(reverse("core:home"))    
```

# url template tag

- html에서 내부적으로 reverse()를 사용할 때 쓴다.

```html
<li><a href="[% url 'blog:post_detail' post.id %}">[[ post.title }}</a> </li>
```

# get_absolute_url()

- **디테일뷰를 설정**할 때 사용할 수 있다. 코드가 간결해진다는 장점이 있다.


```python
class Post(models.Model):
    # ... (중략)
    def get_absolute_url(self):
        return reverse('blog:post_detail', args=[self.id])
```