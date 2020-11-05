---
layout: post
title: 파이썬 장고 Paginator Class쓰기
category: Django
tags: [python, Django]
comments: Django
---

# 참고

[장고 페이지네이션](https://docs.djangoproject.com/en/2.2/topics/pagination/#django.core.paginator.Paginator.count)

### Paginator

- Pagination에서는 **offset과 Navigator**이 중요했다.

- offset을 구하기 위해서 **page_size(limit)와 current_page**가 있어야 했고, Navigator를 위해서 **block_size와 current_block**이 있어야 한다. `page_count = ceil(models.Room.objects.count() / page_size)`가 있어야 햇다.

- page_size와 current_page로 offset(리스트 시작점 1인지, 6인지, 11인지)이 구해진다. block_size와 current_block을 통해서 offset_page(페이지 시작 1인지 6인지)이 구해진다.

- Paginator에서는 page_size만 주면 된다.

- paginaton은 여러 군데에서 쓰인다. 리스테서도 쓰이고, 리뷰에서도 쓰인다.

- rooms, reviews, list를 반복하기가 귀찮다. 장고는 paginator을 제공한다.

- QuerySets are lazy => 

- room_lists = models.Room.objects.all()이 쿼리셋을 생성한다. print(room_lists)하지 않는 이상 단순히 쿼리셋을 생성할 뿐이다.

- 호출되는 순간에 **데이터베이스**로부터 불러온다. 로딩되지는 않는 쿼리셋이 존재한다.

- paginaotr가 다 해준다. offset, limit등을 다 해준다.

```python
def all_rooms(request):

    # offset역할한다.
    page = request.GET.get("page")
    room_list = models.Room.objects.all()
    paginator = Paginator(room_list, 10)
    rooms = paginator.get_page(page) # 페이지 내용을 가져온다. 
    
    #
    all_rooms = models.Room.objects.all()[offset:limit]

    # Navigator은 전달하지 않았다.
    #count존재한다. # page_count = ceil(models.Room.objects.count() / page_size)
    return render(request, "rooms/home.html", {"rooms": rooms})

```

### Paginator

- 페이지네이터는 페이지를 만들어준다. 기본적으로 페이지는 refrence를 쓴다.

### get_page vs page

- 2가지 메소드가 존재한다. get_page()와 page()가 있다.

- get_page()에서는 해당하는 페이지 번호가 없을 때 첫번째 페이지를 반환한다.

- 반면 page()는 aises InvalidPage if the given page number doesn’t exist.

- 에러처리에 더 유용하다!!!!!!!!!!!!!!!!!!!!!!

# Exception

- try - except를 쓴다. exception이라면 핸들링할 수 있다.

- path는 오로지 url과 함수만 갖는다.  HomeView는 class이다.


### cbv vs fbv

- 뭔가를 삽입할 때는, 페이지네이터같은 걸 계속 코드 복붙하고 싶지 않다. Inheritance를 사용한다.

- 복잡한 폼이 있거나 엘리먼트에 대한 필터링이 있다면 function based view가 필요하다.

- cbc는 한 가지만 할 수 있고 그걸 잘 한다. 방을 목록으로 표시하는 것 하나라면 좋다.

- 모든 view는 get_context_data를 갖고 있다. context는 템플릿으로 가는 변수이다.

- cbc는 매우 유연해서 함수를 추가할 수 있다. 그러나 하드코어한 커늩롤과 뭐가 일어나느지 봐얗나다면 fbv가 좋다.

# 참고

[Making Queries](https://docs.djangoproject.com/en/2.2/topics/db/queries/)

[Builtins](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/)

[QuerySets are lazy](https://docs.djangoproject.com/en/2.2/topics/db/queries/#querysets-are-lazy)

[Paginator](https://docs.djangoproject.com/en/2.2/topics/pagination/)
