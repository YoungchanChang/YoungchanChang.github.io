---
layout: post
title: React create 기능 구현
category: React
tags: [react, create]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24860)를 정리한 글입니다.  
> 모든 정보기술은 crud를 다루는 것이 기본이다.

# 구현 로직

1.컨트롤 컴포넌트 추가(쓰기, 수정 ,삭제 생성)
- 쓰기, 수정은 `<a></a>`태그의 링크로 처리한다.
- 삭제 버튼은 링크로 처리하면 문제가 된다. 페이지가 아니라 버튼으로 해야된다.

```javascript
//./components/Control.js
import React, { Component } from 'react';

class Control extends Component {
    render() {
        return (
            <ul>
                <li><a href="/create">create</a></li>
                <li><a href="/update">update</a></li>
                <li><input type="button" value="삭제"></input></li>
            </ul>
        )
    }
}

export default Control

```

2.컨트롤 컴포넌트의 쓰기 버튼 이벤트 핸들러 설치
- 컨트롤 컴포넌트에서 상위 컴포넌트의 state.mode = "write"으로 변경시키는 event핸들러 설치
- 컨트롤 컴포넌트에 상위 컴포넌트에게 이벤트 핸들러를 통해 `write`라는 정보 전달
    
```javascript
//./components/Control.js
import React, { Component } from 'react';

class Control extends Component {
    render() {
        return (
            <ul>
                <li><a href="/create"
                //onClick메소드가 추가된 코드
                    onClick={
                        function (e) {
                            e.preventDefault();
                            this.props.controlComponent("write");
                        }.bind(this)
                    }
                >create</a></li>
                <li><a href="/update">update</a></li>
                <li><input type="button" value="삭제"></input></li>
            </ul>
        )
    }
}

export default Control

```

3.상위 컴포넌트에서 하위 컴포넌트의 이벤트를 값을 받아서 state값 변경
- 상위 컴포넌트는 하위컴포넌트의 `write`의 정보 값 받아서 this.setState()메소드로 자신의 state에 변경

```javascript
//./components/App.js
    <Control controlComponent={
        function (id) {
        console.log("컨트롤 컴퍼넌트에서 전달받은 값 : " + id);
        this.setState({
            mode: id
        })
        }.bind(this)
    }
    ></Control>
```

4.쓰기 컴포넌트 생성
- form 태그에 onSubmit이벤트를 설치한다. 해당 이벤트는 form태그의 고유한 기능이다.
- 쓰기 컴포넌트에서 제목, 내용의 데이터를 상위 컴포넌트에 전달한다.
- 제목, 내용의 데이터를 event.target(현재 태그를 의미).title(폼안에 태그 name속성).value로 전달

```javascript
//./components/WriteContent.js
import React, { Component } from 'react';

class WriteContent extends Component {
    render() {
        return (
            <article>
                <h2>Create</h2>
                <form onSubmit={
                    function (e) {
                        e.preventDefault()
                        this.props.sendWrite(e.target.title.value, e.target.desc.value)
                    }.bind(this)
                }>
                    <p>
                        <input type="text" name="title" placeholder="title"></input>
                    </p>
                    <p>
                        <textarea name="desc" placeholder="description"></textarea>
                    </p>
                    <input type="submit"></input>
                </form>
            </article>
        )
    }
}

export default WriteContent
```

5.상위 컴포넌트의 state.mode값에 따라서 하위 컴포넌트 변경
- state.mode값에 따라 값을 담을 변수를 생성한다
- state.mode가 `read`면 변수에다가 읽기 컴포넌트를 `write`이면 변수에다가 쓰기 컴포넌트로 변경

```javascript
// ./App.js
    var write = null;
     if (this.state.mode === 'read') {
      write = <Content title={_title} desc={_desc}></Content>;
    } else if (this.state.mode === 'write') {

      write = <WriteContent></WriteContent >;
    }

```

6.상위 컴포넌트에서 쓰기 컴포넌트의 값 처리.
- 상위 컴포넌트에서 글쓰기 컴포넌트에서 입력한 데이터를 state.contents 배열에 추가한다.
- state.contents 배열의 마지막 값 뒤에 추가하기 위해서 마지막 값의 정보를 담는 변수(max_content_id)를 추가한다.
- 여기서 max_content_id는 state안에 넣으면 불필요한 렌더링이 발생하기 때문에 state안에 넣지 않는다.
- concat()으로 글쓰기 컴포넌트의 데이터를 상위 컴포넌트에서 추가한다. concat()을 쓰면 push()와 달리데이터를 추가한 새로운 배열이 생성된다.
- push()를 쓰지 않는 이유는 push()는 원본을 바꾸기 때문이다. 다음 shouldComponentUpdate()에서 자세히 설명
- setState({})에 변경된 데이터를 삽입한다.

```javascript
// ./App.js
    var write = null;
     if (this.state.mode === 'read') {
      write = <Content title={_title} desc={_desc}></Content>;
    } else if (this.state.mode === 'write') {

      write = <WriteContent sendWrite={
        function (_title, _desc) {
          this.max_content_id = this.max_content_id + 1;
          var data = this.state.contents.concat(
            { id: this.max_content_id, title: _title, desc: _desc });
          this.setState({
            contents: data
          })

        }.bind(this)
      }></WriteContent >;
    }

```

# ShouldComponentUpdate

- 글 목록의 리스트가 바뀌지도 않았는데 계속 render()가 발생하면 비효율적이다.
- render()이전에 shouldComponentUpdate()가 수행된다.
- shouldComponetUpdate()의 return값이 true면 reder()메소드 호출 false면 render()메소드 호출되지 않도록 약속되어있다
- 상위 컴포넌트에 새로운 값을 받지 않으면 shouldComponent()의 return값을 false로 줌으로써 `성능 최적화`를 이룰 수 있다.
- shouldComponent(nextProps, nextState)의 nextProps는 상위 컴포넌트에서 새로운 값을 줄 때 쓰인다.
- 단, 여기서 상위컴포넌트에서 주는 값은 복사본이어야 한다. push()를 쓰면 원본이 바뀌기 때문에 해당 메소드가 수행되지 않는다.

```javascript
class TOC extends Component {
//./components/TOC.js
    shouldComponentUpdate(newProps, newState) {
        console.log("TOC Component Rendering")
        if (this.props.data === newProps.data) {
            return false;
        }
        return false;
    }
}
```

# 참조

- [React.Component](https://ko.reactjs.org/docs/react-component.html)
