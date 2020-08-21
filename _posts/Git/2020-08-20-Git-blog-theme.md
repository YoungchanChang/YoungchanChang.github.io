---
layout: post
title: 다른 사람 테마 내 블로그에 적용하기
category: Git
tags: [git, blog]
comments: true
---

> lanyon님의 [테마](http://codinfox.github.io/blog/)를 [초보몽키](https://wayhome25.github.io/)님의 테마로 바꾸는 과정을 기록한 글입니다.

<br>

# 원본 테마 다운받기
1. [원본 테마](http://codinfox.github.io/blog/)를 다운받습니다.
2. 로컬 서버에서 해당 파일을 실행시켜봅니다.

---

# _config.yml수정하기
1. Site Info에서 자신에게 맞는 정보로 변경합니다.
- title은 홈페이지의 제목 역할을 합니다.
- tagline을 상단 헤더의 제목 역할을 합니다.
- logo는 상단 헤더의 로고 이미지입니다.

2. #About/Contact부분 자신이 원하는 정보로 변경
- description에 우측 배너에 보이는 설명입니다.
- contact는 자신에게 연락받을 수단을 설정하는 곳입니다.

3. nav를 자신이 원하는 카테고리로 변경
- nav아래 카테고리들은 우측에 보이는 리스트를 의미합니다.
- 카테고리별로 클릭시 이동하고 싶은 경로로 수정합니다.
  - '/blog'는 클릭시 '/blog/index.html'로 간다는 의미
  - 하위태그의 좌측은 보여지는 이름이고 우측은 클릭시에 태그별로 이동하는 파라미터 값입니다.


4. 카테고리에 데이터 넣어보기
- _post폴더아래에 카테고리 경로를 생성후에 파일을 만들어봅니다.
- 주의할 점은 경로에 한글을 넣으면 안 됩니다.
- 상단에 아래와 같은 코드를 넣습니다.

```markdown
---
layout: post
title: Git블로그에 다른 사람 테마 적용해보기
category: Git
permalink: /Git/:year/:month/:day/:title/
tags: [Git, blog]
comments: true
---
```

- category에 적절한 태그를 입력하면 자동으로 카테고리 태그에 분류가 되어서 보여지게 됩니다.
- tags에 들어가는 값들은 글을 클릭시 글 하단에 태그로 보여지게 됩니다.

---

# 색상변경이나 파일 내용 수정하기

### 1. 테마 색상 변경하기
- _scss폴더 아래에 _config.css에서 $theme-color에 원하는 테마 색상을 설정합니다.

### 2. 헤더의 이미지 변경하기
- _layouts아래에 default.html태그 안에 이미지 원하는 이미지로 변경합니다.

##### _includes에서 sidebar.html에서 sidebar-personal-info-section클래스 태그 안의 내용 변경합니다.

```html
    <!-- 변경전 코드-->
    <a href="http://gravatar.com/{{ site.author.gravatar }}">
      <img src="http://www.gravatar.com/avatar/{{ site.author.gravatar }}?s=350" title="View on Gravatar" alt="View on Gravatar" />
    </a>

    <!-- 변경후 코드-->
    <a href="https://www.github.com/YoungchanChang">
      <img src="/public/profile.png" alt="profile picture" />
    </a>
```

- public폴더 아래에 이미지 파일들을 원하는 이미지로 덮어씁니다.

##### _includes에 sidebar.html파일의 아래의 코드 수정합니다.

```HTML
  <!-- 제거할 코드 -->
  <span class="sidebar-nav-item">Currently v{{ site.version }}</span>

  <!-- 제거할 코드 -->
  <div class="sidebar-item">
    <p>
    &copy; {{ site.time | date: '%Y' }} {{ site.author.name }}. This work is liscensed under <a href="http://creativecommons.org/licenses/by-nc/4.0/">CC BY-NC 4.0</a>.
    </p>
  </div>

  <!-- 추가할 코드 -->
<!-- <div class="sidebar" id="sidebar">태그 안에 <div class="sidebar-personal-info-section"> 세번째 테그의 하단 </p>밑에  이미지 아래에 넣고 싶은 내용 생성 -->
    <span class="notice">
    잘못된 내용이 있다면 편하게 댓글 남겨주세요!
    </span>
```

# 메인 페이지에 내가 쓴 최신글 보이게 하기

- /index.html 폴더에 html뼈대를 추가합니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>

```

- body태그 안에 blog폴더 아래에 categories의 내용을 복사해서 붙여넣습니다.
    - categories는 카테고리 목록을 보여주는 역할로, 제가 쓴 글을 순차적으로 보여주는 역할을 합니다.

```html
<div class="tags-expo">
  <div class="tags-expo-list">
    {% for tag in site.categories %}
    <a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a>
    {% endfor %}
  </div>
  <hr/>
  <div class="tags-expo-section">
    {% for tag in site.categories %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
      <li>
        {{ post.title }}
       <small class="post-date">{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div>

```

-  tags-expo-section 아래에 다음 코드를 붙여넣습니다.
  - 여기서 shortcut.png에 이미지의 경로를 확인하세요!
  - 가장 상단의 a태그는 태그의 제목을 의미한다.
  - for안의 내용은 _posts안에 있는 내용을 0부터 10까지 불러오라는 뜻이다. 그러면 최신 글이 순서대로 불러와진다.

```html
  <div class="tags-expo-section">
    <!-- 추가된 내용 -->
      <a href="/blog/">
        <h4 id="shortcut"><img id="shortcut-img" src="/public/shortcut.png">최근 글 바로가기</h4>
      </a>
      <ul class="tags-expo-posts">
        {% for post in site.posts offset: 0 limit: 10  %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
          <li>
            {{ post.title }}
            <small class="post-date">{{ post.date | date_to_string }}</small>
          </li>
        </a>
        {% endfor %}
      </ul>
    <!-- 추가된 내용 끝-->

    {% for tag in site.categories %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
    <ul class="tags-expo-posts">
      {% for post in tag[1] %}
        <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
      <li>
        {{ post.title }}
       <small class="post-date">{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
```

마지막으로 style태그 안에 css를 변경합니다.

```html
  <!-- jquery 추가 -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
  <style>
    .category-title {
      cursor: pointer;
    }

    .category-title:hover>h2 {
      text-decoration: underline;
    }

    .tags-expo-posts {
      display: block;
    }

    #shortcut {
      font-size: 1.1rem;
      color: rgba(49, 49, 49, 0.82);
    }

    #shortcut-img {
      width: 30px;
      display: inline;
      margin-right: 9px;
      vertical-align: -webkit-baseline-middle;
    }
  </style>

```