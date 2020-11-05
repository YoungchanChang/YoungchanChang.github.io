---
layout: post
title: 파이썬 장고 Pagination과 PHP비교
category: Django
tags: [python, Django]
comments: Django
---

# Pagination PHP

- offset과 limit을 통해서 데이터 리스트를 가져온다.

- block을 통해서 페이지네비게이션을 구한다.

```php
    // 맨 처음 들어왔을 때 값 처리예외처리
    $current_page = 1;
    if (isset($_GET['page'])) {
        $current_page = $_GET['page'];
    }

    // 1. offset구하는 부분
    $limit = 5;
    $offset = ($current_page - 1) * $limit;
    $list_sql = "SELECT * from bbs ORDER BY bbsID DESC LIMIT $offset, $limit;";
    $show_data = mysqli_query($link, $list_sql);
    $show_rows = mysqli_num_rows($show_data);


    // 반복문을 통해서 가져온 데이터를 $offset지점부터 출력한다.
    for ($i = $offset; $i <= $show_rows; $i++) {
        $fetch = mysqli_fetch_array($show_data);
        <tr>
            <td><?= $i ?></td>
            <td><a href="view.php?bbsID=<?= $fetch['bbsID'] ?>"><?= $fetch['bbsTitle'] ?></a></td>
            <td><?= $fetch['userID'] ?></td>
            <td><?= $fetch['bbsDate'] ?></td>
        </tr>
    }

    // 2. 네비게이션바 보여주는 부분
    // MySQL에서 총 행의 수를 가져온다.
    $link = mysqli_connect('localhost', 'root', '123456', 'bbs');
    $sql = "SELECT * from bbs";
    $result = mysqli_query($link, $sql);
    $num_rows = mysqli_num_rows($result); #총 행의 수

    $block_size = 5;
    $page_count = ceil($num_rows / $limit);
    $total_block = ceil($page_count / $block_size); # 블락 수 제어를 위해 쓰임

    $current_block = ceil($current_page / $block_size); // 0, 1, 2, 3, 4의 값이 나올 수 있다.
    $s_page = ($current_block * - 1) * ($block_size) + 1; // +1을 하는 이유는 사용자에게 0부터 보여질 수 없기 때문이다.
    $e_page = $current_block * $block_size;
    if ($page_count <= $e_page) {
        $e_page = $page_count;
    }

    // 페이지 순서대로 보여주기
    for ($page = $s_page; $page <= $e_page; $page++){
        <li class="page-item"><a class="page-link" href="bbs.php?page=<?= $page ?>"><?= $page ?></a></li>
    }
```

# 장고 

- page_count는 반올림을 한다.

- page를 두번 주는 이유는 request URL이 `&page=`일 때, get으로 값을 가져오지 않는 불완전한 문제가 발생할 수 있다.

```python
    page = request.GET.get("page", 1)
    page = int(page or 1)
    page_size = 10
    limit = page_size * page
    offset = limit - page_size
    all_rooms = models.Room.objects.all()[offset:limit]

    #Navigatior 간단한 버전
    page_count = ceil(models.Room.objects.count() / page_size) # total_page를 block으로 나눈뒤 start, end_page를 구하면 위와 같다.
    
    return render(
        request,
        "rooms/home.html",
        {
            "potato": all_rooms,
            "page": page,
            "page_count": page_count,
            "page_range": range(1, page_count),
        },
    )
```

```html
    [5 for page in page_range 5]
        <a href="?page={{page}}">{{page}}</a>
    [5 endfor 5]
```

# 추가로 알아두어야 할 사항

- 이전페이지로 가는 것은 current_page와 연관있다.

- php에서

```python
    if ($current_page != 1) {
    ?>
        <li class="page-item"><a class="page-link" href="bbs.php?page=<?= $current_page - 1 ?>">Previous</a></li>
    <?php
    }

    if ($current_block < $total_block) {
    ?>
        <li class="page-item"><a class="page-link" href="bbs.php?page=<?= $current_page + 1 ?>">Next</a></li>
    <?php
    }
```

- 장고에서

```html
    {5 if page is not 1 5}
        <a href="?page={{page|add:-1}}">Previous</a>
    {5 endif 5}

    Page {{page}} of {{page_count}}

    {5 if not page == page_count  5}
        <a href="?page={{page|add:1}}">Next</a>
    {5 endif 5}
```

# 참고

[Pagination](https://www.quora.com/What-is-pagination)
