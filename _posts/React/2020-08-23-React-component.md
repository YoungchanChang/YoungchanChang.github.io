---
layout: post
title: React 컴포넌트 만들기
category: React
tags: [react]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24737)를 정리한 글입니다.  
> '강사로부터 독립'하기 위해서는 1.**설명서(API 문서)**를 보고 2. **도구**를 이용해서 스스로 설명서를 이해한다. 3. 질문, 검색한다.

# 컴포넌트 만드는 방법(정말 중요)

### 리액트 컴포넌트의 필요성

- 만약 header 태그안의 내용이 만줄 정도 된다면 코드가 한 눈에 들어오지 않게 된다. **정리 정돈**해서 이름만 갖고 오면 가독성이 증가하게 된다. 리액트의 컴포넌트를 쓰면 **가독성**을 늘리는 역할을 한다.

- 참고로 시맨틱 태그는 리액트와 상관없는 html5스펙이다. 기능은 없고 태그를 보고 해당 내용이 무엇(네비게이션인지, 기사인지)알 수 있게 해준다.

### 컴포넌트 만들기

1. 클래스를 만들고 Component클래스를 상속한다. 클래스 안에 render()메소드를 구현한다.
    - 컴포넌트에서는 **반드시** render() 메소드가 있어야 한다.

2. render()메소드의 return 값으로 태그를 넣는다
    - 컴포넌트는 하나의 최상위 태그로 시작해야한다.

3. 컴포넌트가 필요한 자리에 아래와 같은 코드를 삽입하면 된다.

```html
<컴포넌트 이름></컴포넌트 이름>
```

3. 실제 웹 페이지를 보면 태그가 반영되는 것을 볼 수 있다.
    - 리액트는 컴포넌트를 html로 바꿔주는 역할을 한다.

### 컴포넌트 속성값 주기

- html 태그들은 이름과 속성이 있다. 태그의 속성값을 다르게 줌으로써 태그들을 여러가지로 활용할 수 있다.
    - 예를 들어서 `<a href="1index.html"></a>`에서 a태그 이름의 속성값 href의 값 1index.html을 다른 값으로 바꿀 수 있다.

- 컴포넌트도 태그와 마찬가지로 속성값을 주어서 **사용자 정의 태그**를 만들 수 있다. 컴포넌트는 속성을 **props**라고 부른다.

- 속성값 주기

1. 속성값을 반영하고 싶은 곳에 `{this.props.속성이름}`을 쓴다.

```javascript
class Subject extends Component {
    render(){
        return{
            <header>
                <h1>{this.props.title}</h1>
            </header>
        }
    }
}
```

2. 컴포넌트 선언시 속성값을 준다.

```html
<Subject title="WEB"></Subject>
```


### React Debugger 활용하기

1. [React Developers Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)에서 크롬 리액트 디버깅 툴을 다운받는다.

2. 크롬을 전부 껐다가 다시 키고 리액트 페이지로 들어간다.
    - 만약 전부 안 끄면 반영이 안될 수 있다.

3.  `F12`를 누르고 우측 상단의 Components탭을 연다.

### Component 파일로 분리하기

1. src디렉터리 아래에 새 디렉터리를 생성한다.

2. 파일을 생성하고 상단에 `import React, { Component } form 'react';`를 붙여넣는다.
    - 해당 코드는 컴포넌트관련 라이브러리를 불러오는 코드이다.

3. 컴포넌트를 작성한다.

4. 파일 안에서 `export default '클래스명'`을 통해 클래스를 외부에서 사용할 수 있게 허용한다.

5. 컴포넌트를 쓰는 쪽에서는 `import 이름 from "디렉터리경로/클래스명"`을 통해 해당 클래스를 쓰겠다고 선언한다.

