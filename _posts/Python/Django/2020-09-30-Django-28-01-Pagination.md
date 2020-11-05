---
layout: post
title: 파이썬 장고 Pagination
category: Django
tags: [python, Django]
comments: Django
---

# Pagination

### Why Pagination

- 페이지네이션이란 전체 콘텐트를 쪼개는 것을 의미한다.

- 1.사용자 경험 증가 - 사용자 입장에서 너무 많은 정보는 사용자에게 패닉을 안겨다 줄 수 있다.

- 2.서버의 부담 감소 - DB에 1만개의 데이터가 있다면 한번에 다 불러오는 것은 트래픽을 증가시킬 수 있다. 따라서, 필요한 일부분만 불러오는 것이 효율적이게 된다.

- 페이지네이션의 단점 : SEO에는 좋지 못 하다.

### Pagination

- Pagination을 하기 위해서는 SQL문의 offset과 limit을 알아야 한다. 아래 SQL문에서 offset시작점에서, limit만큼 가져오는 것이 pagination이 된다.

```console
SELECT 칼럼명1, 칼럼명2
      [FROM 테이블명 ] # 생략가능
      [GROUP BY 칼럼명] # 생략가능
      [ORDER BY 칼럼명 [ASC | DESC]] # 생략가능
      [LIMIT offset, limit] # 생략가능
# offset은 시작점, limit은 가져올 행의 수를 의미한다.
```

### offset(페이지의 내용을 가져올 시작점) - current_page와 page_size

- offset을 구하기 위해서는 2가지 개념이 필요하다. **current_page와 page_size**

- 내가 클릭한 현재 페이지(current_page)에서 limit(page_size)만큼 가져오게 된다.

- 리스트 보여주기 : Page는 DB에서 불러오는 지점이다. **DB의 기준점**이 된다. page_size는 기준점으로부터 **불러오는 사이즈**다.

    - offset구하기 방법 1 ((current_page - 1) * page_size)을 하면 offset을 구할 수 있다. -1을 붙인 이유는 값은 0부터 시작하기 때문이다. 아래는 php로 구현한 예시이다.

```php
    // 1. offset구하는 부분
    $offset = ($current_page - 1) * $page_size;
    $list_sql = "SELECT * from noticeboard ORDER BY noticeId DESC LIMIT $offset, $page_size;";
    $data_show = mysqli_query($link, $list_sql);
```

    - offset구하기 방법 2 (limit = page_size * page)를 하면 최대 맥시멈 값이 나온다. (offset = limit - page_size)를 하면 값이 나온다. limit을 offset식에 대입하면 방법 1과 같은 값이 나오게 된다.

```python
    page_size = 10
    limit = page_size * page
    offset = limit - page_size
    all_rooms = models.Room.objects.all()[offset:limit]
```

    - PHP에서는 SQL문을 직접적으로 이용하기 때문에 limit만큼의 값을 가져오는 것이 좋은 반면, 장고에서는 objects.all()[offset:limit]으로 배열을 통해 가져오기 때문에 두번째 방법을 쓰는 것이 좋다.

### block(페이지 네비게이션을 가져올 시작점) - page와 block

- 네비게이션 - Block은 한 블록에서 보여지는 **페이지의 양**이다.

    - (current_page/block)을 하면 (0, 1, 2, 3)등의 값이 나온다. (0, 1, 2, 3)*block을 하면 어느 페이지부터 보여줄지 정해질 수 있다.

```php
    // 2. 네비게이션바 보여주는 부분
    $current_block = ceil($current_page / $block);  // 0, 1, 2, 3, 4의 값이 나올 수 있다.
    $s_page = ($current_block - 1) * ($block) + 1; // +1을 하는 이유는 사용자에게 0부터 보여질 수 없기 때문이다.
    $e_page = $current_block * $block;

    // 끝 지점 정하기
    $total_page = ceil($num_rows / $list);
    if ($total_page <= $e_page) {
        $e_page = $total_page;
    }

```

### 추가로 고려해야 할 사항

- page를 처음 방문했을 때, default값으로 page=1로 줘야한다. PHP에서는 아래와 같이 설정한다.

- 해당값은 Previous선택에 영향을 미친다.

```php
    $current_page = 1;
    if (isset($_GET['page'])) {
        $current_page = $_GET['page'];
    }

    if ($current_page != 1) {
    <li class="page-item"><a class="page-link" href="bbs.php?page=<?= $current_page - 1 ?>">Previous</a></li>
    }
```
- 장고에서는 아래와 같이 설정한다.

```python
    page = int(request.GET.get("page", 1))

    {% if rooms.has_previous %}
        <a href="?page={{rooms.number|add:-1}}">Previous</a>
    {% endif %}
```

- 마지막 값이 블록의 끝값이어야 한다.

```php
    // 끝 지점 정하기
    $total_page = ceil($num_rows / $list);
    if ($total_page <= $e_page) {
        $e_page = $total_page;
    }

    // 끝페이지까지 페이지 보여주기
    for ($page = $s_page; $page <= $e_page; $page++) {
```

# 참고

[Pagination](https://www.quora.com/What-is-pagination)
