---
layout: post
title: React update & delete
category: React
tags: [react, event]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24861)를 정리한 글입니다.  

# 참조
[리액트 폼](https://ko.reactjs.org/docs/forms.html)


- update는 read와 create결합이다. CREATE form안에 READ처럼 데이터를 가져와야 한다.

- 기본 로직
- READ를 클릭하면 해당되는 글의 id값이 저장된다.**ID값이 현재 저장되어있음**
- update버튼을 클릭하면 create FORM에 저장된 id의 값이 반영된다.

- 상세 로직
- 1.글 리스트 버튼 클릭 후(글 내용이 보인다) 업데이트 버튼 클릭시 create폼태그 안에서 내용이 보이게 하기
- 업데이트 컴포넌트를 만든다. CREATE form을 UPDATE form으로 가져온다.

```javascript
import React, { Component } from 'react';

class UpdateContent extends Component {

    render() {
        console.log("Content Rendering")
        return (
            <article>
                // 업데이트임을 알려줘야한다.
                <h2>UpdateContent</h2>
                <form onSubmit={
                    function (e) {
                        e.preventDefault()
                        this.props.sendWrite(e.target.title.value, e.target.desc.value)
                    }.bind(this)
                }>
                    <p><input type="text" name="title" placeholder="put title please..."></input></p>
                    <p><textarea name="desc" placeholder="put desc please..."></textarea></p>
                    <input type="submit"></input>
                </form>
            </article>
        )
    }
}

export default UpdateContent
```

- 업데이트 컴포넌트에 props로 줄 값? 저장된 id값에 따른 title, desc를 전달한다.
- 컨트롤 컴포넌트에 업데이트 클릭시 state.mode=='update'로 만든다. 해당 모드에 따라 {content}를 업데이트 컴포넌트로 바꾼다.

```javascript
else if (this.state.mode === 'update') {

    //글 목록을 불러오는 코드. READ와 같다.
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


      mode = <UpdateContent
        //데이터를 전달한다.
        updateDate={data}
      ></UpdateContent>

      
    }

```
- 그러면 업데이트 버튼 클릭했을 때 이미 값이 있는 것이 보인다.

- 2.값 입력했을 때 변경시키기
- props는 read-only이기 때문에 props값(id, title, desc)을 state에 저장시킨다.
- input값에 value는 변하지 않는다. onChange메소드 안에서 setState({})메소드 안에서 내용 변경을 구현해야 한다.
- id는 히든 값으로 처리해야 한다. textarea에 value={this.state.desc}로 설정한다.
- update에 대한 식별자를 건네줘야한다. 폼에서 ID는 히든 form으로 한다.
- `<input type="hidden" name="id" value={this.state.id}></input>`으로 인풋값 설정 id값도 준다.

```javascript
import React, { Component } from 'react';

class UpdateContent extends Component {

    constructor(props) {
        super(props);
        this.state = {
            id: this.props.updateDate.id,
            title: this.props.updateDate.title,
            desc: this.props.updateDate.desc
        }
    }

    render() {
        return (
            <article>
                <h2>Update</h2>
                <form onSubmit={
                    function (e) {
                        e.preventDefault()
                        this.props.sendWrite(e.target.id.value, e.target.title.value, e.target.desc.value)
                    }.bind(this)
                }>
                    <p><input type="hidden" name="id" value={this.state.id}></input></p>
                    <p><input type="text" name="title" value={this.state.title}
                        onChange={
                            function (e) {
                                this.setState({
                                    title: e.target.value
                                })
                            }.bind(this)
                        }
                    ></input></p>
                    <p><textarea name="desc" value={this.state.desc}
                        onChange={
                            function (e) {
                                this.setState({
                                    desc: e.target.value
                                })
                            }.bind(this)
                        }
                    ></textarea></p>
                    <input type="submit"></input>
                </form>
            </article>
        )
    }
}

export default UpdateContent

```

- 3.submit버튼으로 제출됬을 때 내용 수정하기
- READ처럼 현재 ID값을 받아서 교체한다. READ는 그냥 읽기만 하고, UPDATE는 CREATE처럼 Array.from()으로 한다.
- 배열이나 객체 수정하려고 할 때는 해당 객체를 복사해서 수정한다.
- id값에 따라서 글을 출력하는 while문과 똑같이 하되, 해당 배열의 id값의 데이터를 바꾸는 것으로 한다.

```javascript
      mode = <UpdateContent
        //이게 맞나????
        updateDate={data}
        sendWrite={
          function (_id, _title, _desc) {
            console.log(_id, _title, _desc)

            var _contents = Array.from(this.state.contents);

            var i = 0;
            while (i < _contents.length) {
              if (_contents[i].id === Number(_id)) {
                _contents[i] = { id: Number(_id), title: _title, desc: _desc };
                break;
              }
              i = i + 1;
            }

            this.setState({
              contents: _contents
            })

          }.bind(this)
        }
      ></UpdateContent>
```





- 리팩토링하기
- 리팩토링 1. 컴포넌트의 리팩토링
- !!!메소드를 나눠라!!! this.getContent()로 하면 return값 그대로 쓸 수 있다. 보기가 훨씬 좋다!!!
- getReadContent() return값은 data로 한다. var content =  this.getReadComponent(); 이런식으로 쓰면 좋다.

```javascript
  getReadContent() {
    var i = 0;
    while (i < this.state.contents.length) {
      var data = this.state.contents[i];

      if (data.id === this.state.selected_content_id) {
        return data;
      }
      i = i + 1;
    }
  }

  if (this.state.mode === 'read') {
      var _content = this.getReadContent();

      mode = <Content title={_content.title} desc={_content.desc}></Content>
  } else if (this.state.mode === 'update') {
      _content = this.getReadContent();
      mode = <UpdateContent
      updateDate={_content}></UpdateContent>
  }

```



- 리팩토링 2. 읽기컴포넌트의 리팩토링
- render()아래가 너무 많다.

```javascript

  getReadComponent() {
    var _title, _desc = null;
    var mode = null;

    if (this.state.mode === 'Welcome') {
      _title = this.state.welcome.title;
      _desc = this.state.welcome.sub;
    } else if (this.state.mode === 'read') {
      var _content = this.getReadContent();
      mode = <Content title={_content.title} desc={_content.desc}></Content>


    } else if (this.state.mode === 'write') {
      mode = <WriteContent ></WriteContent>


    } else if (this.state.mode === 'update') {
      _content = this.getReadContent();
      mode = <UpdateContent></UpdateContent>

    }
  }
  render() {

    {this.getReadComponent()}
  }


```


- 리팩토링 2. onChange메소드의 리팩토링

```javascript
inputFormHandler(e){
    this.setState({[e.target.name]:e.target.value})    
}
```

-  bind.(this)를 하기 위해서는 constructor에서 bind.(this)로 묶어줄 수 있다. REFACTORING!!~!~!

- [e.target.name]은 최신 자바스크립트 문법이다. 객체 리터럴이라고 하며,
- []안의 내용이 객체의 속성명으로 바로 사용될 수 있다.
- const newObject = { [es+6] : 'Fantastic' }, console.log(newObject.ES6)
