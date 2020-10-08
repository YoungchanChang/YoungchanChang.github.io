---
layout: post
title: 파이썬 장고 AdminPanel
category: Django
tags: [python, Django]
comments: Django
---

# 관리자 페이지

- 장고는 관리자페이지를 자동으로 만들어준다. 나의 모델로부터 metatdata를 읽어서모델중심의 인터페이스를 만들게 도와준다. 관리자는 조직의 내부 관리에 효율적으로 쓸 수 있다. 전체 프런트엔드까지 관리를 하는 것은 아니다.

- list_dispaly는 보여지는 `열(column)`을 보여준다.

- list_filter은 필터로 거르고 싶은 열들을 보여준다. search_fields는 검색할 열들을 알려준다. **필터는 순서가 중요**하다.

- search_fields는 검색창을 만들어준다.

### search_fields의 팁

- search_fields는 서치박스를 관리자 페이지에서 검색할 수 있게 해준다. 열(field)의 이름이어야 한다.

- ForeignKey나 ManyToManyField를 오른쪽과 같이 이용해서 검색할 수 있다. `search_fields = ['foreign_key__related_fieldname']`

- 만약 검색 필드에서 ` ['first_name', 'last_name'] `으로 설정하고 사용자가 `john lennon`을 검색했다면, SQL문을 쓰는 구문에서 아래는 예시이다.

```python
WHERE (first_name ILIKE '%john%' OR last_name ILIKE '%john%')
AND (first_name ILIKE '%lennon%' OR last_name ILIKE '%lennon%')
```

- 검색어를 쓸 때 Prefix로 다음과 같은 값을 쓰면 좋다. Prefix는 ^로 startswith를 의미한다. 

|Prefix|Lookup|
|------|---|
|^|startswith|
|=|iexact|
|@|search|
|None|icontains|



- 검색어는 None	icontains이 기본 값이다.

- 특정 검색어가 없을 시 다음 열로 찾을 수 있다. 여기에서 foreingkey로 접근하는 방법은 `search_fields = ['foreign_key__related_fieldname']`이다.

- Advanced options'은

### fields옵션

- fields옵션은 레이아웃의 부분만을 보여줄 수 있게 해준다. fieldsets와 같이 쓰일 수 있다.

- fielsets는 "add"와 "change"페이지를 컨트롤해준다. fieldsets는 2개의 튜플로 이루어져있으며, 각 튜플은 name, fieldoptions)로 이루어진다. name은 필드셋의 이름이며, 필드옵션은 딕셔너리 형태의 정보를 제공한다.

### filter_horizontal

- `filter_horizontal옵션`은 수정 페이지에서ManyToManyField에서 multiple-select boxes를 해줄 수 있게 해준다.

- 사용자 정의 함수는 정렬이 되지 않는다. 첫번째 인자는 자기 자신을 가리키는 객체이고, 두번째 인자는 row를 의미한다.

- ordering은 정렬이 가능하게 된다.


### Room admin 추가기능

- 함수를 이용하고, 함수명을 통해 새로운 정보를 반환할 수 있다.

- 집계함수처럼 특정 목록의 숫자를 보여준다던지, 시작과 끝의 차이를 보여줄 수 있다.

# 참고

[model admin options](https://docs.djangoproject.com/en/2.2/ref/contrib/admin/#modeladmin-options)

[Meta Option 복수형](https://docs.djangoproject.com/en/2.0/ref/models/options/)

[ordering](https://docs.djangoproject.com/en/2.0/ref/models/options/#ordering)