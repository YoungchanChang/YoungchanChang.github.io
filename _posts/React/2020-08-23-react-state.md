---
layout: post
title: react state
category: react
tags: [react]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24738)를 정리한 글입니다.  


# state란?

- 하나의 제품을 바라볼 때 사용자 입장과 구현자 입장이 있다. 아이폰을 예로 들면 사용자 입장은 화면을 터치하는 것이고, 구현자 입장은 내부 부품들을 만드는 것이다.

- 리액트의 관점에서는 props기능은 사용자의 입장에서 컴포넌트를 조작을 도와주는 기능이다. 반면 **state기능은 구현자 입장에서 컴포넌트 조작을 도와주는 기능**이다.

- 리액트에서 좋은 Component를 만들기 위해서는 사용자를 위한 props기능과 구현자를 위한 state가능이 철저히 분리되어있어야 한다.

# state의 사용

1. constructor를 이용해 컴포넌트의 값을 초기화 한다.

2. constructor 내부에 `this.state = {}` 코드를 적고 안에 초기화 하고 싶은 값들을 넣는다.
    - 여기서 상위 컴포넌트 state값은 하위 컴포넌트 props로 전달 가능하다.

- 예시)

```javascript
class App extends Component{
    constructor(props){
        super(props);
        this.state = {
            subject : {title:"WEB", sub:"World Wide Web!"}
        }        
    }
    render(){
        return(
            // 상위 컴포넌트(App)의 state값을 하위 객체에 전달
            <Subject
            title={this.state.subject.title}
            sub={this.state.subject.sub}>
            </Subject>
        )
    }
}

```

# state를 쓰는 이유

- state를 쓰면 컴포넌트의 **사용성**이 증가한다.
    - 만약 글 목록을 보여주는 컴포넌트가 있다면 props를 통해서 글 목록 데이터를 받을 수 있게 된다.
    - 글 목록 관련 컴포넌트를 쓰는 구현자는 상위 컴포넌트의 state값을 설정한 뒤 하위 컴포넌트의 props에 전달할 수 있다.
    - 그러면, 상위 컴포넌트에서 하위 컴포넌트 데이터를 관리할 수 있게 되는 장점이 있다.

- 예시)
    - 아래 클래스에서 TOC클래스의 역할은 글의 목록을 보여주는 역할이다.
    - 해당 클래스의 데이터를 직접 건드리지 않고 상위 객체에서 관리하기 때문에 사용성이 증가하게 된다.
    - 여러개의 엘리먼트를 자동으로 생성하기 위해서는 **"key" prop(식별자)**이 필요하다.

```javascript

class TOC extends Component {

    render() {
        console.log('TOC render');

        //1. this.props.data를 통해 데이터를 받는다.
        var data = this.props.data;

        //2. lists배열에 해당 데이터를 순서대로 넣는다.
        var lists = [];
        var i = 0;
        while (i < data.length) {
            lists.push(
                
        //3.여러개의 엘리먼트를 자동으로 생성하기 위해서는 key prop이 필요하다.
                <li key={data[i].id}>
                    <a
                        href={"/content/" + data[i].id}
                        data-id={data[i].id}
                    >{data[i].title}</a>
                </li>);
            i = i + 1;
        }
        return (
        
        //4. 배열을 원하는 위치에 둔다.
            <nav>
                <ul>
                    {lists}
                </ul>
            </nav>
        );
    }
}

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      subject: { title: 'WEB', sub: 'World Wid Web!' },
      contents: [
        { id: 1, title: 'HTML', desc: 'HTML is for information' },
        { id: 2, title: 'CSS', desc: 'CSS is for design' },
        { id: 3, title: 'JavaScript', desc: 'JavaScript is for interactive' }
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

        // 글 목록이 변한다면 APP객체에서 데이터만 변화시키면 된다.
        <TOC data={this.state.contents}></TOC>
        <Content title="HTML" desc="HTML is HyperText Markup Language."></Content>
      </div>
    )
  }
}

```
