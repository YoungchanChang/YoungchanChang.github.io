---
layout: post
title: React update & delete
category: React
tags: [react, event]
comments: true
---

> 본 글은 [생활코딩 react](https://www.opentutorials.org/module/4058/24861)를 정리한 글입니다.  

# Update설명
- update는 read와 create결합이다. CREATE form안에 READ처럼 데이터를 가져와야 한다.

### update의 기본 로직
- Update의 로직은 읽기 -> 수정 -> 저장 순서로 이루어진다.
- 읽기 : 데이터를 먼저 읽는다.(글의 id값이 저장된다.)
- 수정 : 읽은 데이터를 수정한다.(Create과 같은 form에 읽은 데이터가 반영된다.)
- 저장 : 수정한 데이터를 저장한다.(수정한 값이 저장된다.)


### update의 상세 로직
- 1.준비 : 업데이트 컴포넌트
- 업데이트 컴포넌트를 만든다. UPDATE form은 CREATE form으로 가져온다.

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

- 2.읽기 : 읽는 글에 따른 제목, 내용을 업데이트 컴포넌트에 props값으로 준다.
- 컨트롤 컴포넌트에 업데이트 클릭시 state.mode=='update'로 만든다. 그리고 {content}를 업데이트 컴포넌트로 바꾼다.

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
- 확인 : 업데이트 버튼 클릭했을 때 이미 값이 있는 것이 보인다.

- 3.수정 : 값 입력했을 때 변경시키기
- onChange메소드와 setState({})메소드로 입력된 값을 변경시킨다.
- onChange메소드 : 
- input값에 value는 변하지 않는다. onChange메소드 안에서 setState({})메소드 안에서 내용 변경을 구현해야 한다.
- setState({})메소드 " 
- props는 read-only이기 때문에 수정이 불가능하다. 따라서, props값(id, title, desc)을 state에 저장시킨다.
- 추가 사항
- id값이 필요하다. 글 수정을 했을 때 몇번 글을 수정할 것인지 식별자를 건네줘야하기 때문이다. id는 히든 값으로 처리해야 한다. 
- textarea에 value={this.state.desc}로 설정한다.

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

- 4.저장:수정된 데이터에서 id, 제목, 내용을 받아서 수정한다.
- 배열이나 객체 수정하려고 할 때는 해당 객체를 복사해서 수정한다. Array.from()메소드를 쓴다.
- 내용을 update할 때는 해당 배열의 id값의 데이터의 제목, 내용을 바꾸는 것으로 한다.

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
- 리팩토링 1. 메소드의 리팩토링
- 메소드를 나누기 this.getContent()로 하면 return값 그대로 쓸 수 있다. 보기가 훨씬 좋다!!!
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


- 리팩토링 3. onChange메소드의 리팩토링

```javascript
inputFormHandler(e){
    this.setState({[e.target.name]:e.target.value})    
}
```

-  bind.(this)를 하기 위해서는 constructor에서 bind.(this)로 묶어줄 수 있다. REFACTORING!!~!~!

- [e.target.name]은 최신 자바스크립트 문법이다. 객체 리터럴이라고 하며,
- []안의 내용이 객체의 속성명으로 바로 사용될 수 있다.
- const newObject = { [es+6] : 'Fantastic' }, console.log(newObject.ES6)



# React Delete

# Delete의 기본 로직
- 데이터를 Read로 읽는다. 해당 글의 id에 따라 데이터를 삭제한다.
- 정말 삭제할지 물어본다.

```javascript
        function (id) {
          if (id === "delete") {
            if (window.confirm('really?')) {
              var _contents = Array.from(this.state.contents);

              var i = 0;
              while (i < _contents.length) {
                if (_contents[i].id === this.state.selected_content_id) {
                  _contents.splice(i, 1);
                  break;
                }
                i = i + 1
              }

            }
          }
          
          this.setState({
                mode: 'welcome',
                contents: _contents
              })
        }.bind(this)
```

# 참조
[리액트 폼](https://ko.reactjs.org/docs/forms.html)

