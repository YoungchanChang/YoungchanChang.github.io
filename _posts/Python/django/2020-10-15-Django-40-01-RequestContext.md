---
layout: post
title: 파이썬 장고 RequestContext
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[Request Context](https://docs.djangoproject.com/en/3.1/ref/templates/api/#django.template.RequestContext)

# Context

- 장고는 뷰에서 **템플릿에 데이터를 전달**하기 위해 context를 쓴다. 장고에서는 RequestContext를 쓴다. RequestContext는 기존 Context와 다르게 **첫번째 인자로 request**를 쓴다. 또한, context_processor를 사용해서 컨텍스트에 **변수를 추가**한다.

- context_processor는 `request object`를 인자로 받은 뒤에 context에 dictionary로 통합시킨다.

# RequestContext에 값 추가하기

- 예를 들어서 아래의 코드와 같이 request를 받은 뒤에 딕셔너리로 값을 추가할 수 있다.

```python
from django.template import RequestContext

request_context = RequestContext(request)
request_context.push(["my_name": "Adrian"})
```

- 아래와 같이 추가 요청처리를 진행할 수 있다. 

```python
from django.http import HttpResponse
from django.template import RequestContext, Template

def ip_address_processor(request):
    return ['ip_address': request.META['REMOTE_ADDR']}

def client_ip_view(request):
    template = Template('[[ title }}: [[ ip_address }}')
    context = RequestContext(request, [
        'title': 'Your IP Address',
    }, [ip_address_processor])
    return HttpResponse(template.render(context))
```

- 해당 데이터에 대해서 처리하기 위해서 context_processor를 쓴다. 예를 들어서 장고에서 RequestContext에 대해서 `django.template.context_processors.csrf`는 활성화 되어 있는데 이 기능은 보안상 FORM에서 들어온 값이 유효한지 아닌지 확인하는데 쓰인다.

- 모든 처리 과정에서 context는 변수의 이름을 통해 전달된다. 변수의 이름이 같다면 override된다. 

# 다양한 context_processor

- `django.contrib.auth.context_processors.auth`에서 auth()메소드는 현재 로그인한 유저와 허락상태를 나타낸다.

- `django.template.context_processors.debug`에서 DEBUG가 True이고 IP address가 INTERNAL_IPS 세팅 안에 있을 때 활성화된다. sql_queries는 모든 SQL쿼리에 대해 요청과 얼마나 걸렸는지 알려준다.

- `django.template.context_processors.i18n`는 언어 관련 내용을 처리한다. (https://docs.djangoproject.com/en/3.1/topics/i18n/translation/#i18n-template-tags) 참고

- `django.template.context_processors.media`는 MEDIA_URL을 사용한다.