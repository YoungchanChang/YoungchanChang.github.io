---
layout: post
title: 파이썬 장고 sizes 
category: Django
tags: [python, Django]
comments: Django
---

# 참고
[Looping over the form's fields](https://docs.djangoproject.com/en/2.2/topics/forms/)

# Login Social

- 아이템들을 배치할 생각을 해야한다. 여러개의 아이템이 있을 때, 부모의 관계를 명시한다.

- display flex를 쓰면 정렬을 할 수 있다.

- width, height는 절대값 아니면 상대값으로 결정된다.

- 상대값은 부모와의 관계에서 상대적으로 결정된다.

# -or-을 만들기

- 핵심은 `<class="flex items-center">`를 주면 된다.

- `w-full`로 주게 되면, 값이 결정이 안 되어있다. 나중에 결정이 된다.

- 박스모델로 

- 아이템을 정 가운데 배치하는 tip

```html
justify-content: center;
align-item: center;
```

# 

- form태그 안에서 input태그 주기

- 장점 : 코드가 깔끔해진다. model폼을 이용할 수 있다.

- 아래에는 password필드에 에러를 추가한다.

- None으로 적으면 non_field_error가 된다.

```python
else:
    self.add_error("password", forms.ValidationError("Password is wrong"))
```

# General Field Errors

- input에 대해서 error메시지를 빨간색으로 반응하게 만들기

- `&.has_error`라고 하면 has_error가 있는 db일 경우 반응한다.

- `&의 의미는?` - div의 input에 has_error라는

### 개꿀팁

- css에서 꾸밀 때 &.has_error은 `form. input.has_error`과 같다. space없으면 input과 has_error가 같이 있을 때를 의미한다.

- 두 클래스가 같은 공간안에 있어야 한다. input과 함께 있을 때만 효과가 발휘된다!!!

- `space를 입력하면 input 안에 has_error가 있는 경우를 의미한다.`

###

- `forms.ModelForm과 UserCreationForm의 차이는?`

## 장고에서 템플리 폴더화 할 때 고려해야 할 사항

- 재활용 될 수 있는 부분인가? => 부분으로 만든다.

- 변수들이 들어있는가?(관리가 필요하다)자주 쓰이는가?

###

- 파트 쪼갠 뒤에 서로 연결되는 부분이 잘 와닿지 않는다. HTML CSS도 다루어야한다.

- 파일들을 다룰 때 제일 골치아픈것? 경로가 절대경로가 아니다. .env처럼 절대경로가 필요하다.

- 변수로 url을 준다.