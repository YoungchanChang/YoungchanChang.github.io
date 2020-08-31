---
layout: post
title: javascript-08 Closure
category: javascript
tags: [javascript, closure]
comments: true
---

> 본 글은 [생활코딩](https://opentutorials.org/course/743/6544)강의를 요약, 정리한 글입니다.  

# 클로저

### 클로저란?

- 내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것을 클로저라고 한다. 

### 왜 클로저를 쓸까?

- 자바스크립트에서 **변수를 private으로 쓸 때** 쓰인다. 변수를 private으로 만들면 정보를 아무나 수정하도록 하는 것을 방지할 수 있다. 많은 데이터가 S/W안에서 존재하는데, **누구나 수정할 수 있으면 해당 S/W가 망가질 가능성이 크게** 된다. 

### 클로저를 쓰는 방법

- 아래의 예제에서 title은 지역변수이다. title의 지역변수는 return된 객체의 메소드(get_title, set_title)만으로 접근이 가능하다. 

- factory_movie라는 외부 함수 자체는 호출과 동시에 소멸이 됬기 때문에 지역변수인 title은 factory_movie의 내부함수인 get_title()와 set_title()을 통해서만 접근이 가능하다.

- set_title()에서는 값을 검증할 수 있다.

```javascript
function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function(_title){
            if(typeof _title === 'String'){
                title = _title
            } else {
                alert('제목은 문자열이어야 합니다.');
            }

        }
    }
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
 
alert(ghost.get_title());
alert(matrix.get_title());
 
ghost.set_title('공각기동대');
 
alert(ghost.get_title());
alert(matrix.get_title());
```


### 반드시 알아야할 사항

- 함수 안에 또 다른 함수를 선언하는 것을 **내부함수**라고 한다. 내부함수를 쓰는 이유는 그 함수에서만 사용하기 때문에 **응집성이 증가**한다.

- 내부함수는 **외부함수의 지역변수에 접근**할 수 있다.

- 아래 예제에서 내부함수는 inner(), 외부함수는 outter()이다.


```javascript
function outter(){
    var title = 'coding everybody';  
    function inner(){        
        alert(title);
    }
    inner();
}
outter();
```

### 추가로 알아야 할 사항

- 클로저를 쓰기 위해서 **외부 함수의 지역변수 값을 내부 함수가 참조해야 한다.**.  외부 함수가 없다면 클로저를 쓸 수 없고, 지역변수가 아니라면 쓸 수 없다. 따라서 클로저를 쓰기 위해서는 내부 함수로 만들어야 한다.

- 예시 코드

```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id) {
        return function(){
            return id;
        }
    }(i);
}
for(var index in arr) {
    console.log(arr[index]());
}
```

# 참고
[클로저](https://opentutorials.org/course/743/6544)