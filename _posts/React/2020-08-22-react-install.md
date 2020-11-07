---
layout: post
title: react 개발환경 구축하기
category: react
tags: [react]
comments: true
---

> 본 글은 [생활코딩 React](https://www.opentutorials.org/module/4058/24666)강의를 요약, 정리한 글입니다.  

# 개발환경 구축하기
개발환경 구축순서는 NPM깔기 -> CreateReact App깔기 -> 개발환경 완성하기

> NPM이란? NodeJS기술을 이용한 앱들을 명령어로 손쉽게 설치하는 도구입니다.
> NodeJS계의 **구글 앱스토어 역할**을 하는 s/w입니다.  

### NPM 깔기
1. [Node.js공식 홈페이지](https://nodejs.org/ko/)에서 다운로드 받아서 설치합니다.
2. 윈도우 cmd창에서 `npm -v` 명령어를 입력해 npm이 설치 되었는지 확인합니다.  

### create-react 앱 설치하기
cmd창에서 `npm install -g create-react-app`로 설치합니다.
- 이 문장의 뜻은 npm이라는 프로그램에 create-react-app이라는 어플리케이션을 컴퓨터 어디서든(-g) 실행할 수 있게 설치(install)해달라는 명령어입니다.

- 만약 EACCESS오류가 뜬다면 권한이 없는 것으로 `sudo npm install create-new-app`명령어로 실행시켜봅니다.

> `npx install -g create-react-app`명령어를 통해 설치할 수 있습니다.  
> npm과 달리 npx는 프로그램을 임시로 설치하는 명령어입니다. 한번만 실행시키고 지웁니다.  
> npx의 장점은 컴퓨터 공간을 낭비하지 않고, 설치하는 앱을 항상 최신상태를 유지할 수 있습니다.

### react-app 개발 환경 구축하기
1. 개발을 하고 싶은 디렉터리에 `react-app`이름으로 폴더명을 짓습니다.
- 폴더명은 굳이 react-app이 아니어도 되지만, react라는 폴더명으로 지으면 안 됩니다.

2. 커맨드 창에서 cd 하고 해당 경로를 드래그 드랍합니다.
- 여태까지 cd하고 경로 복사붙여넣기 했는데 이런 좋은 방법이 있었다니!!!

3. cmd창에서 `create-react-app .`명령어를 치시면 개발 환경이 구축됩니다.

- 아래와 같이 명령어를 수행해도 됨

```console
E:\GitHub\react>npx create-react-app react_test
```

# react로 코드 작성하기

### 샘플 앱 실행하기

1. vscode코드 에디터의 상단의 View -> Appearance -> Show Panel(단축키 Ctrl+J)를 누르면 하단에 터미널 창이 생깁니다. 터미널을 통해서 명령어로 컴퓨터를 제어할 수 있습니다.

2. 하단의 터미널에서 npm [run] start로 샘플 앱을 실행시켜봅니다.

3. 터미널 창에 아래와 같은 코드가 출력됩니다.
```
  Local:            http://localhost:3000        
  On Your Network:  http://192.168.44.1:3000  
```
4. 해당 주소로 들어가면 앱이 개발되는 모습을 확인할 수 있습니다.


### react에서 JS로 코드 작성해보기

- 리액트에는 디렉터리 구조에는 크게 src, public이 있습니다. public의 index.html파일이 있는데 웹 브라우저에서 보이는 파일이 이 index.html파일입니다.

- index.html파일에서 중요한 부분은 `<div id="root"></div>`부분입니다. 리액트에서 만든 컴포넌트들이 `<div id="root"></div>`안에 들어가기 때문입니다.

- 컴포넌트들은 src디렉터리안의 파일들을 수정해서 만듭니다. 우리가 만드는 대부분의 파일들은 src디렉터리에 넣게 됩니다.

- src디렉터리에서 진입점은 index.js라는 파일입니다. 해당 파일에서 `document.getElementById('root')`부분은 index.html파일의 `<div id="root"></div>`부분에 반영되게 됩니다.

- index.js파일에서 `<App />`부분은 react를 통해 만든 사용자 정의 component입니다. 실제 구현은 상단의 `import App from './App';`를 통해 이루어지게 됩니다. 이 문장은 `./App`파일의 이름을 App이름으로 쓰겠다는 것입니다. 그래서 `<App />`을 `<Apple />`로 바꾸고 싶다면, 상단의 `import App from './App';`도 `import Apple from './App';`로 바꿔야 됩니다.

- 사용자가 정의한 App.js파일의 컴포넌트의 반영이 실제 웹에 반영되어서 나오게 됩니다. 따라서 App.js파일의 내용을 수정하면 웹도 반영되어서 나오게 됩니다. 여기서 중요한 점은 react의 바깥쪽에는 태그가 있어야 한다는 점입니다. 이름은 App이 아니어도 됩니다.

### React에서 css수정하기

- React에서 css는 파일 진입점인 index.js파일의  `import './index.css';`부분을 통해 반영됩니다. 따라서, css를 변경하기 위해서는 index.css파일을 수정합니다.

- 컴포넌트의 디자인을 수정하기 위해서는 컴포넌트 파일이 읽는 css파일을 수정해야 합니다.

# React 배포하는 법

- 웹 브라우저에서 `F12`버튼을 누른 뒤 `Network`탭에서 Disable Cache에 체크를 한 뒤 `F5`버튼을 눌러서 웹을 새로고침 해 봅니다.

- 브라우저에서 서버로부터 받은 총 용량이 1.7MB정도 나오는데, 개발의 편의성을 위해 추가로 넣은 기능들이 있어서 용량이 커지게 된 것입니다.

- 배포 목적으로 빌드를 하기 위해서 터미널 창에서 `npm run build`명령어를 칩니다. 그러면 build이름의 디렉터리가 추가됩니다.

- build디렉터리에 index.html를 보면 공백이 없고 읽을 수가 없습니다. 이것은 앱이 실제 production환경에서 사용되는 앱을 만들기 위해서 이미 index.html파일이 갖고 있느 불필요한 공간 정보를 삭제했기 때문입니다.

- 실제 서비스를 구동하기 위해서는 이 build디렉터리 안에 있는 파일들을 쓰면 됩니다. 웹서버의 documentroot에서 build파일 안에 있는 파일들을 위치시키면 실 서버 환경이 완성이 됩니다.

- `npm install -g serve`를 쓰면 컴퓨터 어디에서나 serve명령어를 통해 웹 서버를 설치할 수 있습니다.

- `npx serve -s build`명령어는 한 번만 실행시킬 웹 서버를 다운받아서 실행시킵니다. 여기서 -s옵션은 build라는 디렉터리르 document루트로 하겠다는 뜻입니다.

- 터미널 창에 나오는 주소로 들어가서 다운받은 용량을 확인해보면 이전 용량(1.7MB)보다 작게 나온 것을 볼 수 있습니다.




# 참조

<https://opentutorials.org/module/4047>  
<https://www.opentutorials.org/module/4058/24666>