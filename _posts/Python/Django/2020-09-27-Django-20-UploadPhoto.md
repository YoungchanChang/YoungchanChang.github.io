---
layout: post
title: 파이썬 장고 User Uploads part One
category: Django
tags: [python, Django]
comments: Django
---

# Photo

- Photo를 이용해서 저장한다고 해도, 사진이 불러와서 보여지지 않는다.

- photo가 upload되는 destnation을 바꾼다.

### config에서 환경설정 - 업로드 될 사진이 위치할 폴더

- config/settings.py 에서 MEDIA_ROOT를 설정한다. 파일을 업로드하면 uploads폴더가 생성되있다.

- MEDIA_ROOT는 **업로드 파일들을 관리**하기 위한 경로이다.

```python
MEDIA_ROOT = os.path.join(BASE_DIR, "uploads")
```

### .gitignore설정

- .gitignore에서 필요없는 파일은 삭제한다.

```python
.DS_Store
uploads/
```

### PhotoClass 설정 - upload_to

- ImageField에서 upload_to를 쓰면 **어떤 폴더에다가 photo를 업로드 할 것인지** 정할 수 있다.

```python
class Photo(core_models.TimeStampedModel):
    """ Photo Model Definition"""

    caption = models.CharField(max_length=80)
    file = models.ImageField(upload_to="room_photos")
    room = models.ForeignKey("Room", related_name="photos", on_delete=models.CASCADE)

    def __str__(self):
        return self.caption
```

- 유저 객체에서도 변경해준다

```python
    avatar = models.ImageField(upload_to="avatars", null=True)
```

# 장고 이미지 권한

- 파일은 폴더 경로로 저장이 될 수 있지만, 아직 이미지 파일을 클릭했다면 사진이 보여지지 않는다.

- `Photo with ID "3/change/room_photos/2020-09-15-logistic.png" doesn't exist. Perhaps it was deleted?` 메시지가 뜬다.

- 장고에게 media폴더로 가면 uploads경로에서 쓸 수 있다고 알려줘야 한다.

- MEDIA-URL을 확인해야한다. MEDIA_URL은 MEDIA_ROOT으로 넘어온 미디어를 다룬다.**uploads 디렉토리를 MEDIA_URL과 연결**한다.

- 내가 MEDIA_URL에 뭐라고 적든 MEDIA_ROOT에 나온 "uploads/"를 다룬다.

- 데이터를 가져올 때는 /media/~로 시작해야한다.

- config/settings.py에 `MEDIA_URL = "/media/"`를 추가한다. "media/"앞에 /가 있는 것은 파일을 **절대경로**로 만들어준다. 없다면 **"/admin/media/~~~"**로 가야한다.내가 URL시작에서부터 갖는 의미가 된다.

- 장고가 사진을 어디다 저장할지 알고(**MEDIA_ROOT**), 어떤 url에서 photo를 찾을 수 있는지 안다**MEDIA_URL**. 장고에게 photo를 보여달라고 해야한다.

# 경로 설정

- settings/urls.py 장고에게 어떻게 폴더안의 파일들을 제공할지 가르친다.

- **파일들을 서버 폴더에 저장하지 않아야 한다**. 서버에 트래픽이 많이 발생하면, 문제가 생긴다. production 환경에는 넣지 않고 서버 코드에서 사용자 파일들을 저장하지 않는다. Amazon s3등을 사용한다.

- `from . import settings`를 쓰지 않는다. 파일명이 바뀔 수 있기 때문이다. 파일을 반영한 것을 import해야한다.

- production인지 develop인지는 settings.의 `DEBUG = TRUE`를 확인하면 된다. DEBUG는 오류가 났을 때 노란 페이지를 보여준다.

- 라우터를 생성했다. path를 리턴하고 있다. settings.MEDIA_URL을 폴더의 문서와 연결했다.

- static파일이나 업로드 파일들은 서버에서 사용하지 말아야 한다. 사용자가 많아지면 서버에서 더 많은 디스크 공간을 사용하게 된다.

- static파일들을 제공하는 헬퍼를 사용해야한다.

- **URL/media는 media_root안으로** 들어가야 한다.

```python
from django.contrib import admin
from django.urls import path
from django.conf import settings

urlpatterns = [
    path("admin/", admin.site.urls),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
# Photo Admin

- 파일은 많은 것을 갖고 있다. dir(obj.file)을 해 보면 width, write, url등을 갖고 있다. 프린트해서 보는 것이 전부가 아니다.

- ImageField에 의해서 접근을 갖을 수 있다.

- 장고는 sercurity를 다루는데 준비가 매우 잘 되어있다. 너가 모든 input을 지워야 한다.

- 장고는 이상한 html을 쓰는 것으로부터 보호해줄 수 있다. 사람들이 모든 입력에 대해서 처리하지 않아서 문제가 생긴다.

### 에러코드

- 에러 코드 : You are trying to add a non-nullable field 'file' to photo without a default; 

- 원인 : DB 모델을 수정할 때 기존에 존재하던 정보들을 어떻게 수정할지 정하지 않았기 때문에 발생(null=True)로 설정하면 된다.

- 에러코드 : The empty path didn't match any of these.

- 해결책 : localhost:8000/admin으로 가라

# 참고

[MEDIA_ROOT](https://docs.djangoproject.com/en/2.2/ref/settings/)

[에러코드 해결책](https://has3ong.tistory.com/238)

[URL_patterns](https://docs.djangoproject.com/en/2.2/ref/urls/#django.urls.path)