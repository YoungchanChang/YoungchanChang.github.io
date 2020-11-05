---
layout: post
title: react event
category: react
tags: [react, event]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24740)를 정리한 글입니다.  

# 이벤트의 개념

### 이벤트의 필요성

- event는 react의 props, state를 활용하여 웹 페이지를 역동적으로 만들어주는 기술이다.

- 이것이 가능한 이유는 react에서 props나 state값이 바뀌면 해당 컴포넌트와 하위 컴포넌트의 render()함수가 호출되도록 약속되었기 때문이다.
    - render()은 HTML을 그리는 것을 정의하는 메소드이다.

- 예시) 아래 코드에서 App 컴포넌트의 state값중 mode의 값이 바뀌면 하위 컴포넌트의 `Subect, TOC, Content`의 render()함수가 호출된다.

```javascript
class App extends Component {

  constructor(props) {
    super(props);
    this.state = {
      mode: 'read',
      welcome: { title: 'Welcome', desc: 'Hello, React!!!' },
      contents: [
        { id: 1, title: 'HTML', desc: 'HTML is for information' },
        { id: 2, title: 'CSS', desc: 'CSS is for information' },
        { id: 1, title: 'Javscript', desc: 'Javscript is for information' },
        { id: 1, title: 'React', desc: 'React is for information' },
      ]
    }
  }

  render() {
    return (
      <div className="App">
        <Subject
          title={this.state.subject.title}
          sub={this.state.subject.sub}>
        </Subject>
        <TOC data={this.state.contents}></TOC>
        <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    )
  }
}
```
### 태그에 이벤트 설치하기

- 태그를 클릭했을 때 경고창 메시지 발생 이벤트 설치

1.  태그에 클릭 이벤트 속성값을 주면 된다.
    - JSX규칙상 속성값은 `onClick={ }`형태로 준다.

2. 태그안에 익명함수를 작성하고 그 안에 경고창 메시지 함수를 띄운다.
    - 함수는 `function(){ alert(hi); }`형태로 작성한다.

3. 태그의 기본 동작을 막기 위해서 event.prevenDefault()코드를 가장 먼저 수행시킨다.
    - 이벤트 함수는 기본 parameter로 event값이 있다.
    - 이벤트 함수에 event를 매개변수로 적고 console.log(event)를 적거나 debugger코드를 적으면 확인 가능.
    - event.preventDafault()를 하면 태그의 기본 동작을 막는다.


### 이벤트에서 state 변경하기

1. 이벤트 함수가 끝난 직후에 .bind(this)를 추가한다.
    - 콜백메소드내에서는 this가 기본적으로 동작하지 않는다.
    - bind함수의 매개변수로 객체를 전달하면 콜백함수 내에서 this로 해당 객체를 쓸 수 있다.
    - 여기서 this는 컴포넌트 자신을 의미한다.
    - bind함수의 원리는 [여기](https://www.youtube.com/watch?v=o7Id7GMcuFo&feature=emb_title)에 나와있다.

2. `this.setState(mode:'welcome');`을 추가한다.
    - 이 코드가 state값을 변경하는 react의 규칙이다.

# 컴포넌트와 이벤트

### 컴포넌트 이벤트 만들기

- 헤더를 클릭했을 때 웰컴 메시지로 바꾸게 하기

1.컴포넌트 사용자는 컴포넌트에 state값 변경하는 함수 등록(콜백메서드 등록)
    - 사용하는 컴포넌트는 bind(this)로 사용되는 컴포넌트에게 전달되어야 한다.

```javascript
<Subject
    title={this.state.subject.title}
    sub={this.state.subject.sub}
    onChangePage={function () {
    this.setState({ mode: 'welcome' });
    }.bind(this)}>
</Subject>
```

2.컴포넌트 내부에서 this.props.함수();로 등록된 함수 처리.

```javascript
class Header extends Component {
    render() {
        console.log("Header Rendering")
        return (
            <header>
                <h1><a href="/"
                    onClick={function (e) {
                        e.preventDefault();
                        this.props.onChangePage();
                    }.bind(this)}
                >{this.props.title}
                </a> </h1>
                {this.props.sub}
            </header>
        )
    }
}
```

3.등록된 함수가 수행되면 상위 컴포넌트의 state값이 변함

4.state값에 따라서 메시지 값 변경

```javascript
    var _title, _desc = null;
    if (this.state.mode === 'welcome') {
      _title = this.state.welcome.title;
      _desc = this.state.welcome.desc;
    } else if (this.state.mode === 'read') {
      _title = this.state.contents[0].title;
      _desc = this.state.contents[0].title;
    }

    <Content title={_title} desc={_desc}></Content>

```


### 이벤트로 컴포넌트 상호작용 해보기

- 글 목록을 클릭했을 때 글 내용이 바뀌게 하기
 
1.id값을 컴포넌트에게 받았을 때 state의 특정 값을 id값으로 변경하는 콜백 메소드 등록

```javascript
<TOC data={this.state.contents}
    onChangePage={function (id) {
    this.setState({
        mode: 'read',
        //기본 컨텐츠 값을 변경한다.
        selected_content_id: Number(id)
    });
    }.bind(this)}>
</TOC>
```

2.컴포넌트 내부의 링크를 클릭했을 시 특정 id값을 콜백메소드에게 전달
   - 이벤트 객체의 target속성은 해당 이벤트가 발생한 태그를 가리킨다.

```javascript
<a href={"contet/" + data[i].id}
    data-id={data[i].id}
    onClick={function (e) {
        e.preventDefault();
        this.props.onChangePage(e.target.dataset.id);
    }.bind(this)}>
    {data[i].title}
</a>
```

3.클릭을 했을 때 state값이 변경

4.state값에 따라서 메시지 값 변경

```javascript
    var i = 0;
    while (i < this.state.contents.length) {
    var data = this.state.contents[i];
        if (data.id === this.state.selected_content_id) {
            _title = data.title;
            _desc = data.desc;
            break;
        }
    i = i + 1;
    }
```

# 참조
- [리액트 이벤트 공식문서](https://ko.reactjs.org/docs/handling-events.html)

