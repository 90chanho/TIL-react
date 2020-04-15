# TIL

### [프리페어링 학습]

- Github 저장소 생성(repository name : TIL-react)
- Git Kraken 설치 & GitHub 저장소 클론
- GitHub 저장소에 변경 사항 커밋 후 푸시

---

<details>
<summary>

## 1주차 - 월요일 학습

</summary>
<div>

### [React 학습에 앞서 공부해야 할 것들]

학습 완료

### [Front-End 개발 학습 로드맵]

리액트 학습하면서 같이 학습해야 할 목록

- CSS Architecture 중 BEM
- Module Bundler 중 Webpack

### [프로그래밍 언어 환경]

- React는 최신 Javascript 언어를 적극적으로 사용

### [프레임워크를 사용하는 이유]

1. 모듈 프로그래밍

- 각 기능별로 JS 파일을 구분하기 때문에 코드 해석 및 유지보수가 편리하다.
- 각 JS 파일 내에 의존성 JS 파일을 참조하여 사용하기 때문에, HTML 파일 내에서는 최종 JS 파일 하나만 불러와 화면 로드 속도가 향상된다.

2. 컴포넌트 시스템

- 반복적인 또는 비슷한 내용의 컨텐츠의 경우 컴포넌트화 하면 재사용하기에 편리하다.(작업속도 향상, 유지보수 편리)

### [미숙한 ES6 문법 학습]

[Class]
기본 문법

```
class 클래스명 {
  // 생성자 함수
  constructor () {}
  // static method
  static 함수명 () {}
  // instance method
  함수명 () {}
}

또는 클래스 식으로도 표현 가능

const 변수명 = class {
  // 위와 동일
}
```

ES5와 ES6의 차이

```
// ES5
function Class1 () {
  console.log('생성자 함수 실행')
}
// static method
Class1.init() = function () {}
// instance method
Class1.prototype.open = function () {}
Class1.prototype.close = function () {}

// ES6
class Class1 {
  constructor () {
    console.log('생성자 함수 실행')
  }
  // static method(class method)
  static init () {}
  // instance method
  open () {}
  close () {}
}
```

비공개 데이터 관리 '심볼 + 게터/세터 활용'

```
let _bean = Symbol('bean');

class Coffee {
  constructor (bean) {
    this[_bean] = bean;
  }
  get pea () {
    return this[_bean];
  }
  set pea (new_bean) {
    this[_bean] = new_bean;
  }
}

const ros = new Coffee('rostring')
console.log(ros.bean) // undefined
console.log(ros.pea) // 'rostring'
```

Class 상속

```
class 클래스명 extends 참조할 클래스 {
  constructor (param) {
    // 상위 클래스에서 constructor가 있고 자신도 constructor가 있다면,
    // 반드시 상위 클래스의 constructor를 실행해야 한다.
    super()
  }

  // 상위 클래스와 동일한 이름의 인스턴스 메서드를 가지고 있을 경우
  // 메서드를 오버라이드 할 수 있음
  open () {
    // 상위 클래스의 open 메서드 실행
    super.open()
    console.log('하위 클래스의 open 메서드 실행')
  }
}
```

[정리]

- class는 중괄호({})를 사용하고, 콤마(,)를 사용하지 않는다.
- class 내부에 변수를 선언할 수 없다.
- class의 스태틱 메서드(클래스 메서드)는 클래스 객체를 생성하지 않고도 사용할 수 있다.
- class는 호이스트 되지 않는다.
- 관례적으로 \_(언더스코어)로 시작으로하는 변수명은 비공개(Private) 데이터를 의미한다.
- class를 참조할 때, 상위 클래스와 하위 클래스 모두 constructor가 있다면, 하위 클래스의 constructor에서 반드시 super()를 호출함으로써 상위클래스의 constructor를 실행시켜야 한다.
  </div>
  </details>

---

<details>
<summary>

## 1주차 - 화요일 학습

</summary>
<div>

### [ React 소개 ]

학습 완료

### [ React 러닝 다이어그램 ]

학습 완료

### [ React 컴포넌트와 요소 ]

React Component(= 함수형 컴포넌트)

```
function App () {
  return <div>React Element</div>
}
```

React Element(JSX 사용)

```
var app = <App />
```

ReactDOM - rendering

```
// ReactDOM.render(가상DOM(React Element), 실제DOM)
ReactDOM.render(app, document.querySelector('#app'))
```

### [ React 컴포넌트 구조 이해 및 활용 ]

MenuListItem 컴포넌트 정의

```
function MenuListItem () {
  return <li>List Item</li>
}
```

MenuList 컴포넌트 정의 및 MenuList 컴포넌트 안에서 MenuListItem 컴포넌트 사용

```
function MenuList() {
  return <ul className="ediya-menu reset-list">
    <MenuListItem />
  </ul>
}
```

AppMain 컴포넌트 정의 및 AppMain 컴포넌트 안에서 MenuList 컴포넌트 사용

```
function AppMain() {
  return <main className="app-main">
    <h2 className="a11y-hidden">이디야 음료</h2>
    <MenuList />
  </main>
}
```

App 컴포넌트 정의 및 App 컴포넌트 안에서 AppMain 컴포넌트를 사용

```
function App() {
  return <AppMain />
}
```

[정리]

1. 컴포넌트는 JSX 문법을 사용
2. 함수형 컴포넌트 내에서 요소를 return 할 때 개행을 위해 괄호 사용 가능

### [ React 컴포넌트와 전달 속성(props) ]

컴포넌트에 커스텀 속성을 전달

```
<MenuListItem image="이미지경로" caption="캡션">
```

함수의 매개변수로 속성을 바인딩

```
function MenuListItem (props) {
  console.log(props) // {image: '이미지경로', caption: '캡션'}
  return (
    <li>
      <figure>
        <img src={props.image} />
        <figcaption>{props.caption}</figcaption>
      </figure>
    </li>
  )
}
```

### [ React 프로젝트 생성 with CRA ]

학습 완료

### [ React 프로젝트 디렉토리 구조 - CRA ]

1. public : 정적 리소스 디렉토리

- manifest.json : 웹 앱을 사용자의 장치에 설치할 때 사용되는 메타 데이터를 제공
- index.html : React앱의 기본 템플릿, public 폴더 URL은 %PUBLIC_URL%로 표현할 수 있다

2. src : 애플리케이션 개발 디렉토리

- index.js : React 앱의 엔트리(entry, 시작이 되는) 파일
- App.js : React 컴포넌트 파일

#

[질문]

1. 일반적으로 화살표 함수의 문법은 아래와 같이 식 또는 문으로 표현할 수 있는데

```
const fn1 = () => {
  statement
}
const fn2 = () => express
```

아래 예제 코드를 보니까

```
<ul>
  {
    array.map(item => (
      <li>...</li>
    ))
  }
</ul>
```

const fn1 = () => () 이런식으로 작성이 되어있는데,
이는 요소가 길어질 경우 개행을 하기 위한 목적인 것은 알겠는데
그럼 이 경우에는 '문(statement)'이 아닌 '식(express)' 인가요?

2. JSX에서는 컨텐츠가 없으면 빈 요소가 아닌 경우에도 빈 요소처럼 표현할 수 있는건가요?

```
<div>
  // <i className="icon icon-close"></i>
  <i className="icon icon-close" />
</div>
```

</div>
</details>

---

<details>
<summary>

## 1주차 - 수요일 학습

</summary>
<div>

### [ VS Code 개발 도구 확장 ]

- Prettier
- Formatting Toggle
- React Snippets
- React Pure To Class
- Auto Import
- Import Cost
- Auto Complete
- Bracket Pair Colorizer2
- Color Highlight & Manager
- Image preview
- Translator

### [ 미숙한 ES6 학습 - Promise ]

프로미스?

```
- 프로미스 객체는 비동기 작업이 맞이할 미래의 성공 또는 실패와 그 결과 값을 나타낸다
- 프로미스는 매개변수로 resolve와 reject을 받는다
- 비동기 작업이 제대로 이행된다면 resolve를 호출하고, 어떠한 이유로 에러가 발생한다면 reject를 호출한다.
```

프로미스 생성자, new 생성자로 생성한다

```
const 변수명 = new Promise((resolve, reject)=>{});
```

프로미스의 상태값

```
fending(대기)   : 연산이 이행되거나 거부되지 않은 상태
fulfilled(이행) : 연산이 성공적으로 실행된 상태
rejected(거부)  : 연산이 어떠한 이유로 실패한 상태
```

프로미스 메서드

```
Promise.all(iterable)
: 다수의 프로미스를 병렬처리 할 수 있다
: 모든 프로미스가 성공했을 경우 모든 프로미스 연산이 끝난 후에 각 프로미스들의 값들로 이루어진 이행 값을 반환한다.
: 중간에 실패한 프로미스 연산이 있을 경우 실패한 프로미스를 즉시 반환한다.

Promise.race(iterable)
: 다수의 프로미스 중 가장 먼저 이행되거나 거절된 프로미스를 반환한다.

Promise.resolve()
: 주어진 이유로 이행하는 Promise 객체를 반환

Promise.reject()
: 주어진 이유로 거부하는 Promise 객체를 반환
```

프로미스 프로토타입 메서드(인스턴스 메서드)

```
Promise.prototype.then()
: 프로미스가 성공적으로 이행됐을 경우 resolve의 값을 받아 실행할 수 있다

Promise.prototype.catch()
: 프로미스가 어떠한 이유로 거부되었을 경우 reject이 값을 받아 실행할 수 있다

Promise.prototype.finally()
: 프로미스의 결과 여부와 관계 없이 프로미스가 처리되면 콜백 함수 실행
```

프로미스 체인(Promise Chain) : 이행된 결과에 대해 연속적인 프로미스 실행

```
const promise = new Promise((resolve, reject)=> {
  resolve(1) // 이행(fulfilled) 상태라 가정하여 resolve 함수를 호출하고 숫자 1을 넘겨줌
})

promise.then(res => {
  console.log(res) // 1, 프로미스 객체의 resolve 함수에서 전달된 값
  return (res + 1)
}).then(res => {
  console.log(res) // 2, 첫번째 then()에서 return된 결과 값
  return (res + 1)
}).then(res => {
  console.log(res) // 3, 두번째 then()에서 return된 결과 값
})
```

프로미스 체인 작업 중 에러가 발생할 경우 처리는 catch() 한 번 작성하면 된다

```
promise.then(res => {
  console.log(res) // 1, 프로미스 객체의 resolve 함수에서 전달된 값
  return (res + 1)
}).then(res => {
  throw Error('두번째 then()에서 에러 발생')
}).then(res => {
  console.log(res) // 3, 두번째 then()에서 return된 결과 값
}).catch(error => {
  console.log(error)
}).finally(() => {
  console.log('콜백 함수 실행')
})

// 1
// Error: '두번째 then()에서 에러 발생'
// 콜백 함수 실행
```

예제 - Promise.all() - 모두 성공

```
const promise = new Promise((resolve, reject)=> {
  resolve(1)
})
const promise2 = new Promise((resolve, reject)=> {
  resolve(2)
})
const promise3 = new Promise((resolve, reject)=> {
  resolve(3)
})
const promiseAll = Promise.all([promise, promise2, promise3])

promiseAll.then(res => {
  console.log(res) // [1,2,3]
})
```

예제 - Promise.all() - 중간 실패

```
const promise = new Promise((resolve, reject)=> {
  resolve(1)
})
const promise2 = new Promise((resolve, reject)=> {
  reject('실패!')
})
const promise3 = new Promise((resolve, reject)=> {
  resolve(3)
})
const promiseAll = Promise.all([promise, promise2, promise3])

promiseAll.then(res => {
  console.log(res)
}).catch(err => {
  console.log(err)
})

// '실패!'
```

예제 - Promise.race() - 모두 성공 일 경우

```
const promise = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.002초')
  },1002)
})
const promise2 = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.001초')
  },1001)
})
const promise3 = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.003초')
  },1003)
})
const promiseRace = Promise.race([promise, promise2, promise3])

promiseRace.then(res => {
  console.log(res)
}).catch(err => {
  console.log(err)
})

// 0.001초
```

예제 - Promise.race() - 실패 케이스가 있는 경우

```
const promise = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.002초')
  },1002)
})
const promise2 = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.001초')
  },1001)
})
const promise3 = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    resolve('0.003초')
  },1003)
})
const promise4 = new Promise((resolve, reject)=> {
  setTimeout(()=>{
    reject('거절')
  },1000)
})
const promiseRace = Promise.race([promise, promise2, promise3, promise4])

promiseRace.then(res => {
  console.log(res)
}).catch(err => {
  console.log(err)
})

// '거절'
```

</div>
</details>

---

<details>
<summary>

## 1주차 - 목요일 학습

</summary>
<div></div>

## [ Virtual DOM ]

가상 DOM 구성과 원리

```
구성
- h.js (virtual-hyperscript) : 가상 DOM tree 생성
- createElement.js : 가상 DOM을 실제 DOM으로 생성하여 실제 DOM에 장착(mount)
- diff.js : 이전/이후 상태를 비교하여 변경사항이 있는지 체크
- patch.js : 변경사항이 발생한 DOM을 실제 DOM 다시 붙임
```

가상 DOM을 사용하는 이유

```
UI는 사용자의 요구에 따라 변해야 하는데, UI가 변경되기 위해 실제 DOM이 다시 렌더링 되는 과정은 컨텐츠가 많을수록 속도가 느려진다.
가상 DOM을 사용할 경우 '상태'를 이전과 비교하여 변경사항이 있으면 해당 부분의 실제 DOM만 업데이트(patch)하므로 보다 속도가 빠르다.
```

## [ JSX -> React 요소 ]

JSX란?

```
- JavaScript Syntax eXtension의 약자. 자바스크립트 언어의 확장
- 구문이 HTML과 유사하다.(HTMl의 문법을 따르는 것은 아님)
```

JSX -> React 요소
JSX는 HTML과 유사한 문법을 사용해 React Element(실제 요소는 아니고 자바스크립트 객체)를 만들 수 있도록 한다.

```
const reactEl = (
  <h1 className="title">리액트 엘리먼트</h1>
)
```

바벨은 JSX 코드를 컴파일하여 React Element 객체를 생성한다.
React는 이 객체를 읽어 들여 가상 DOM을 구성하고, 필요에 따라 실제 DOM에 장착(mount)하여 렌더링 될 수 있도록 한다

```
var headElement = React.createElement(
  'h1',
  { className: 'title' },
  '리액트 엘리먼트'
)
```

[ 정리 ]

- JSX는 필수는 아니지만 권고 사항 (편리성, 가독성)
- 리액트 엘리먼트는 '자바스크립트 객체'이다. DOM 요소가 아니다
- 리액트는 리액트 엘리먼트를 읽어 '가상 DOM'을 구성한다

## [미숙한 ES6 문법 학습 - fetch]

fetch란?

```
- Fetch API를 이용하면 Request나 Response와 같은 HTTP의 파이프라인을 구성하는 요소를 조작하는것이 가능하다.
- fetch() 메서드를 이용하는 것으로 비동기 네트워크 통신을 알기쉽게 기술할 수 있다.
```

fetch 기본 스펙

```
- fetch()로 부터 반환되는 Promise 객체는 HTTP error 상태(HTTP Statue Code : 404 | 500)를 reject하지 않는다.
  대신 ok 상태가 'false'인 'resolve'가 반환되며, 네트워크 장애나 요청이 완료되지 못한 상태에는 reject가 반환된다.

- 보통 fetch는 쿠키를 보내거나 받지 않는다.
- 쿠키를 전송하기 위해서는 자격증명(credentials) 옵션을 반드시 설정해야 한다.(기본 자격증명(credentials) 정책은 same-origin.)
```

fetch 문법

```
fetch(url, { init })
  .then(res => {
    if (res.ok) {
      // 통신 성공
    } else {
      // 통신 실패
    }
  })
  .catch(err => {
    // 네트워크 장애
  })
```

예제 - 자격 증명(credentials)이 포함된 Request 요청

```
fetch('https://example.com', {
  credentials: 'include' // 자격 증명이 포함된 인증서를 보내도록 할 경우
})

fetch('https://example.com', {
  credentials: 'same-origin' // 동일한 origin을 가지고 있을때만 자격증명을 전송하려고 할 경우
})
```

init options

```
method: 'GET' // GET, POST, PUT, DELETE....
headers: {
  'Content-Type': 'application/json'
}
mode: 'same-origin' // no-cors, cors, same-origin
cache: 'default' // default, no-cache, reload, force-cache, only-if-cached
credential: 'same-origin' // include, same-origin, omit
```

예제 - init options 사용

```
fetch(url, {
  method: 'GET',
  headers: {
    'Content-Type': 'image/jpeg'
  },
  mode: 'cors',
  cache: 'default'})
  .then(res => {
    if (res.ok) {
      console.log(res)
    } else {
      console.log('통신 실패')
    }
  })
  .catch(err => {
    throw Error('에러')
  })
```

</div>
</details>

---

<details>
<summary>

## 1주차 - 금요일 학습

</summary>
<div>

### [ 데이터 바인딩이란 ]

```
- React에서는 data를 state에 저장하여 사용한다
- 중괄호({})를 사용하여 HTML 코드에 데이터를 바인딩할 수 있다
- 문(statement)이 아닌 식(expression)을 사용해야 한다
```

### [ 콘텐츠 바인딩과 JavaScript 표현식 ]

```
- JSX 코드의 {}는 JavaScript 표현식을 연산한 '결과 값'을 바인딩한다.(식(Expression)은 항상 값을 반환하기 때문에)
```

### [ 속성 바인딩(style, className) ]

```
속성={데이터}

// 스타일을 직접 바인딩
<li style={{color: red; fontWeight: bold}}>...</li>

// 스타일을 객체로 바인딩
const listStyle = {
  color: red,
  fontWeight: bold
}
<li style={listStyle}>...</li>

// 클래스 동적 바인딩
const borderColor = 'red'
<li className={`bordered bordered-${borderColor}`}>...</li> // li.bordered.bordered-red
```

### [ 조건 문을 사용한 조건부 렌더링 (if, switch문) ]

if문

```
function conditionalRendering (isStrong = false) {
  if (condition) {
    return (
      <strong>리액트 학습하기</strong>
    )
  } else {
    return (
      '리액트 학습하기'
    )
  }
}

const App = (
  <p class="title">
    {conditionalRendering(true)}
  </p>
)
```

switch문

```
function conditionalRendering (count) {
  switch (count) {
    case 1:
      return (
        <p>케이스 1에 해당됩니다</p>
      )
    case 2:
      return (
        <p>케이스 2에 해당됩니다</p>
      )
    case 3:
      return (
        <p>케이스 3에 해당됩니다</p>
      )
    default:
      return (
        <p>디폴트에 해당됩니다</p>
      )
  }
}

function randomCount(number) {
  return number % 4 // 0,1,2,3
}

const App = (
  <div>
    {conditionalRendering(randomCount(Math.floor(100 * Math.random())))}
  </div>
)
```

### [ 조건 식을 사용한 조건부 렌더링 (3항식, 논리연산자) ]

3항식

```
const isList = false

const App = (
  <div>
    {
      isList ? (
        <ul>
          <li>리스트 요소를 반환합니다</li>
        </ul>
      ) : (
        <p>문단 요소를 반환합니다</p>
      )
    }
  </div>
)

```

논리연산자

```
const profile = {
  name: 'chanho',
  home: 'seoul'
}

function Introduce() {
  return (
    <p>{profile.name || '유저1'}</p>
    <p>{profile.home || `한국`}</p>
  )
}
```

### [ Array 객체의 map() 메서드를 활용한 리스트 렌더링 ]

```
const users = [
  {
    name: '찬호',
    home: '서울'
  },
  {
    name: '호찬',
    home: '대전'
  },
  {
    name: '한초',
    home: '대구'
  },
  {
    name: '초한',
    home: '부산'
  },
]

function UserList () {
  return (
    <ul>
      {
        users.map((user, index) => (
        <li key={index}>
        이름 : {user.name}
        사는 곳: {user.home}
        </li>
        ))
      }
    </ul>
  )
}
```

### [ JSX 사용시 주의할 점 ]

```
- 속성 이름은 camelCase를 사용
- 단, 접근성 속성은 hypen-case를 사용
- 콘텐츠가 없는 요소는 처럼 반드시 닫아(</>) 주어야 한다
- 기본적으로 루트 요소는 하나만 사용
- 불필요한 래핑 요소를 피하기 위해서는 아래와 같이 사용하면 된다
  1) import React from 'react'
     <React.Fragment></React.Fragment>

  2) import React, { Fragment } from 'react'
     <Fragment></Fragment>

```

[질문]
JSX를 이용해 리스트 렌더링시 key속성에 고유한 값을 부여하는 것은 필수인데,
여러 개의 배열을 각각 리스트 렌더링 했을 때 각 배열 리스트의 key값을 index로 주었을 경우 에러는 아니더라구요
이 고유한 값은 해당 배열 내에서만 고유한 값이면 문제는 없는걸까요?
고유한 값의 범위가 전체 프로젝트 내에서 인지 아니면 해당 페이지 혹은 배열 내에서 인지 궁금합니다~

</div>
</details>

---

<details>
<summary>

## 2주차 - 월요일

</summary>
<div>

### [ React 함수형 컴포넌트 ]

```
// 매개변수로 props를 전달받아 사용한다
function 함수형 컴포넌트 (props) {
  return (
    <p>{props.title}</p>
  )
}
```

### [ React 클래스 컴포넌트 ]

```
class 클래스컴포넌트 extends React.component {
  constructor(props) {
    super(props)
  }

  // render() 함수를 통해 JSX를 값을 리턴
  render() {
    return (
      ...JSX
    )
  }
}
```

### [ React 컴포넌트 import, export / props ]

컴포넌트 모듈을 내보낼 때

```
// app.js
function App () {
  return (
    ...JSX
  )
}

export default App
```

컴포넌트 모듈을 불러올 때

```
// index.js
import 'App' from './app.js'

function Main() {
  return (
    <App />
  )
}
```

함수형 컴포넌트 props

```
function 함수형컴포넌트(props) {
  return (
    <p>{props}</p>
  )
}
```

클래스 컴포넌트 props

```
import React, {component} from 'react'

class 클래스컴포넌트 extends component {
  render() {
    return (
      // 여기서 this는 클래스를 통해 생성된 인스턴스를 말한다
      <p>{this.props}</p>
    )
  }
}
```

컴포넌트에서 props뿐만 아니라 컨텐츠도 같이 넘겨줄 경우 바인딩 하는 방법
(레이아웃(틀)은 유지하고 일부 컨텐츠만 다르게 적용하고 싶을 때 편함)

```
// index.js

import 'App' from './app.js'

const title = '앱 타이틀'

function Main() {
  return (
    <App title={title}>
      <p>이 컨텐츠도 같이 넘겨줄게</p>
    </App>
  )
}
```

props.children로 전달된 컨텐츠 접근 가능

```
// app.js
import React, {component} from 'react'

export default class 클래스컴포넌트 extends component {
  render() {
    return (
      <React.Fragment>
        <h1>{this.props.title}</h1>
        {this.props.children}
      </React.Fragment>
    )
  }
}
```

[정리]

- 컴포넌트에 전달된 속성(props) 객체는 읽기 전용이다. (수정해서는 안 된다)

### [ React 컴포넌트 관리 (추출) ]

```
- 컴포넌트의 구조가 복잡한 경우 재사용성을 고려하여 잘게 나눠 컴포넌트화 하여 개발하는 것이 좋다
- 초기에는 불필요하게 느껴질 수 있지만, 앱 규모가 커질수록 효율성은 높아짐
```

### [ JavaScript 타입 검사 ]

```
- JavaScript는 동적 타입을 사용하는 프로그래밍 언어이기 때문에, 데이터 타입이 잘못 전달된 경우 오류가 아니다.(타입 검사 필요)
```

### [ PropTypes를 활용해 컴포넌트 props 검사 ]

- PropTypes 패키지는 앱 규모가 큰 경우에는 적합하지 않다.
- 규모가 큰 경우 Flow, TypeScript 사용을 권한다

```
// 패키지 불러오기
import React, {Component} from 'react'
import PropTypes from 'prop-types'

//
class 컴포넌트명 extends Component {
  const {속성1, 속성2, ... , 속성n} = this.props
  render() {
    return (
      ...JSX
    )
  }
}

// 컴포넌트 속성으로 PropTypes 객체를 생성
컴포넌트명.PropTypes = {
  // 속성1의 타입은 배열일 경우에만 통과
  속성1: PropTypes.array,
  // 속성2의 타입은 숫자이며 필수로 전달 받는 속성
  속성2: PropTypes.number.isRequired,
  ...
  속성n: 값,
}
```

### [ PropTypes 속성 기본 값 defaultProps 설정 ]

props의 기본 값 설정

- defaultProps 속성을 설정하면 됨

```
import React, { Component } from 'react'

const Worker = ({ name, career, onCareerUp, isLeave }) => (
  // ...
)

// props 기본 값 설정
Worker.defaultProps = {
  name: '찬호',
  career: 0,
  onCareerUp: () => console.log('커리어 업'),
  isLeave: true
}

export default Worker
```

클래스 필드 활용

- 클래스 컴포넌트는 클래스 필드 제안 문법을 사용할 수 있다
- static 구문 사용

```
class Worker extends Component {
  static PropTypes = {
    name: PropTypes.string.isRequired,
    career: PropTypes.number
  }

  static defaultProps = {
    name: '찬호',
    career: 0
  }
}
```

</div>
</details>

---

<details>
<summary>

## 2주차 - 화요일

</summary>
<div>

### [ 클래스 컴포넌트의 state란? ]

클래스 컴포넌트는 함수형 컴포넌트와 달리 다음과 같은 차이점이 있다

1. 자신만의 상태(state)와 라이프 사이클 훅(life cycle hook)을 가진다.
2. this 키워드 사용할 수 있다

클래스 컴포넌트에서 state값 설정하기

```
class App extends Component {
  constructor () {
    super()
    this.state = {
      data1: [],
      ...
    }
  }

  render() {
    return (
      <div>
        <p>{this.stats.data1}</p>
      </div>
    )
  }
}
```

클래스 필드(class field) 문법

```
class App extends Component {
  state = {
    data1: [],
    ...
  }

  render() {
    ...
  }
}
```

state값 변경하기

```
this.setState({
  key: value,
  ...
}, callback())
```

### [ 컴포넌트 라이프 사이클 훅(Life Cycle Hooks)이란? ]

라이프 사이클 3단계

```
1. 탄생(생성) - 마운팅(Mounting)
2. 성장(갱신) - 업데이팅(Updating)
3. 죽음(제거) - 언 마운팅(Unmounting)
```

알반적인 라이프 사이클 단계별 내용

```
1. 마운팅
constructor -> render -> componentDidMount

2. 업데이팅
constructor -> render -> componentDidUpdate

3. 언 마운팅
                         componentWillUnmount
```

### [ 생성 시점의 라이프 사이클 훅 ]

마운팅

```
constructor()
- 컴포넌트 생성 시점에 호출

static getDerivedStateFromProps(props, state) {
  return
}
- 전달된 상태 및 속성을 가져와 설정하는 시점에 호출
- 컴포넌트 상태(state)를 업데이트 할 수 있다

render()
- 컴포넌트 렌더링 시점에 호출

componentDidMount()
- DOM에 마운트 된 이후 시점에 호출
- 리액트 엘리먼트가 실제 DOM에 마운트 되었기 때문에, 실제 DOM에 접근 가능
- DOM을 수정하면 부작용이 있을 수 있음(state나 props에 변화와 관련 없이 DOM을 변경하기 때문에?)
```

상위 컴포넌트와 하위 컴포넌트의 생성 시점

```
- 상위 컴포넌트의 'render() 이후' ~ 'componentDidMount() 이전' 사이에 하위 컴포넌트의 생성이 시작되면서 하위 컴포넌트의 constructor()가 실행 된다.
- 하위 컴포넌트의 componentDidMount()까지 실행 완료 되면, 그 이후에 상위 컴포넌트의 componentDidMout()가 실행된다.
```

### [ 업데이트, 제거 시점의 라이프 사이클 훅 ]

업데이팅

```
static getDerivedStateFromProps()
- 위의 내용과 동일

shouldComponentUpdate(nextProps, nextState) { return boolean }
- 성능 최적화 용도로 사용 됨
- return값 true일 경우 렌더링, false일 경우 렌더링 취소

render() {}
- 위의 내용과 동일

getSnapshotBeforeUpdate(prevProps, prevState) { reutn ... }
- 컴포넌트 업데이트 전 스냅샷 가져오는 시점에 호출

componentDidUpdate () {}
- 컴포넌트 업데이트 이후 시점에 호출
```

언마운팅

```
componentWillUnmount() {}
- 컴포넌트 제거 예정 시점에 호출
```

### [ 오류 발생 시점의 라이프 사이클 훅 ]

오류가 발생하는 경우에만 호출되는 라이프 사이클 훅

```
static getDerivedStateFromError () { }
- '자손' 컴포넌트 오류 발생 시 호출
- 에러 발생시 state값을 변경하여 다른 JSX를 리턴하도록 조작할 수 있다
```

```
const ErrorComponent = () => { return JSX }
const noErrorComponent = () => { return JSX }

class LifeCycleHook extends Component {
  state = {
    hasError: false // 에러 상태를 나타내는 state, 기본값은 false로 설정
  }

  static getDerivedStateFromError(error) {
    // 에러 발생시 실행되므로 state값을 변경하여 리턴시킨다
    return { hasError = true }
  }

  render() {
    // state.hasError가 true이면 ErrorComponent를 렌더링하도록 분기처리
    if (this.state.hasError) {
      return <ErrorComponent />
    }
    return (
      return <noErrorComponent />
    )
  }
}
```

```
componentDidCatch (error, info) { }
- '자손' 컴포넌트 오류 발생 시 호출
- info 매개변수는 어떤 컴포넌트가 오류를 발생시켰는지에 대한 정보를 가진 componentStack 속성을 가진 객체이다
```

</div>
</details>

---

<details>
<summary>

## 2주차 - 수요일

</summary>
<div>

## [ React 이벤트 핸들링 ]

- 이벤트 속성 이름은 camelCase 문법을 사용

[ 추가 ]

- event.target : 이벤트의 발생 요소 (이벤트 버블링 요소에서 최말단에 해당되는 요소)
- event.currentTarget : 이벤트 생성 위치

## [ React 이벤트 핸들러와 this ]

클래스 컴포넌트 this 참조 방법1 -
.bind(this) 사용

```
class App extends Component {
  constructor () {
    super()
    this.method1 = this.method1.bind(this)
  }

  method1 (e) {
    console.log(this) // this === PreventBrowserDefaultAction {}
  }

  render() {
    return (
      <a href="https://google.com/" onClick={this.method1}>Google</a>
    )
  }
}

또는

class App extends Component {
  method1 (e) {
    console.log(this)
  }

  render() {
    return (
      <a href="https://google.com/" onClick={this.method1.bind(this)}>Google</a>
    )
  }
}

```

클래스 컴포넌트 this 참조 방법2 -
화살표 함수 표현식 사용

```
class App extends Component {
  method1 (e) {

  }

  render() {
    return (
      <a href="https://google.com/" onClick={(e) => this.method1(e)}>Google</a>
    )
  }
}
```

클래스 컴포넌트 this 참조 방법3 (강사님 선호) -
클래스 필드 문법 사용

```
class App extends Component {
  method1 = (e) => {

  }

  render() {
    return (
      <a href="https://google.com" onClick={this.method1}></a>
    )
  }
}
```

이벤트 핸들러와 인자 전달 방법1 (강사님 선호) -
이벤트 객체를 전달

```
<BaseButton
  onClick={ (e) => this.handleClick(id, e) }
>
  ...
</BaseButton>
```

이벤트 핸들러와 인자 전달 방법2 -
.bind(this, arguments)

```
<BaseButton
  onClick={ this.handleClick.bind(this, param) }
>
  ...
</BaseButton>
```

컴포넌트 통신

## [ React 컴포넌트 간 통신이 필요한 이유 ]

학습 완료

## [ 부모 컴포넌트와 자식 컴포넌트 사이의 props ⇌ callback ]

- 부모 컴포넌트는 자식 컴포넌트에게 props로 메서드를 전달
- 자식 컴포넌트는 전달받은 메서드를 실행하여 부모 컴포넌트에게 callback

## [ 복잡한 컴포넌트 트리 구조에서 props ⇌ callback의 문제 ]

- 컴포넌트 중첩이 복잡한 경우 해당 props와 callback을 사용하지 않더라도 각 컴포넌트마다 설정 해줘야 하기 때문에 복잡해진다.

## [ 상태 관리를 효율적으로 관리하기 위한 방법 Context, React Redux ]

복잡한 컴포넌트에서 props와 callback해결책

- Context : 컴포넌트를 재사용할 수 없기 때문에 필요한 경우가 아니면 다른 방법을 사용해야 한다
- State 관리 라이브러리 'Redux' : 공통 저장소를 두고 각 컴포넌트에서 가져다 쓰는 방법

</div>
</details>

---

<details>
<summary>

## 2주차 - 목요일

</summary>
<div>

### [Context의 Provider, Consumer를 사용한 데이터 공유]

- props 전달의 문제점  
  : 컴포넌트의 중첩이 많을 수록 하위 컴포넌트로 prop를 전달하고 상위 컴포는트로 콜백하는 것이 복잡해 짐  
  : Context를 사용하면 전달하고자 하는 props를 가지고 있는 공급자(Provider)역할 컴포넌트와,  
   해당 props를 사용하고자 하는 수요자(Consumer)역할 컴포넌트에서만 작업하면 된다.

```
import React, { Component, createContext } from 'react'

// createContext 객체를 활용하여 context를 생성, ()는 기본값 설정
const AuthContext = createContext(false)

class App extends createContext {
  state = {
    authentification: true
  }

  render() {
    return (
      // 공급자 역할, 전달하고자 하는 props는 value 속성을 사용
      <AuthContext.Provider value={this.state.authentification}>
        <MenuBar />
      </AuthContext>
    )
  }
}

// 수요자가 아닌 컴포넌트는 전달 과정 불 필요.
const MenuBar = () => (
  <SignIn />
)

const SignIn = () => {
  <AuthContext.Consumer>
    {
      // 매개변수로 context를 전달 받음
      (context) => {
        ...
      }
    }
  </AuthContext.Consumer>
}
```

### [Context 모듈을 활용해 개별 컴포넌트에서 데이터 공유]

- Context 또한 별도의 파일로 구분하면 유지보수에 좋음

```
// AuthContext.js

import React, {createContext} from 'react'

export const authContext = {
  isAuth: false,
  signIn = () => { ... }
}

export default createContext(authContext)
```

공급자

```
// App.js
import React, {Component} from 'react'
import AuthContext from './context/AuthContext'

class App extends Component {
  state = {
    authentification: true
  }
  logIn = () => {
    ...
  }
  render() {
    return (
      <AuthContext.Provider value={{ isAuth: this.state.authentification, signIn: this.logIn }}>
        <MenuBar />
      </AuthContext.Provider>
    )
  }
}
```

수요자

```
// SignIn.js
import AuthContext from '../context/AuthContext'

const SignIn = () => (
  <AuthContext.Consumer>
    {
      ({isAuth, signIn}) => isAuth ?
        <div className="signed">로그인 됨</div> :
        <button type="button" onClick={() => signIn}>로그인</button>
    }
  </AuthContext.Consumer>
)
```

### [Context Type 활용]

클래스 컴포넌트와 Context

```
- 'context 객체'를 '클래스 컴포넌트의 스태틱(static) 속성'으로 지정해 활용하는 방법
- <Context.Consumer> 대신 this.context로 접근이 가능하다
```

```
import AuthContext from '../context/AuthContext'

class Signin extends Component {
  static contextType = AuthContext

  render() {
    const {isAuth, signIn} = this.context
    return (
      isAuth ?
        <div className="signed">로그인 됨</div>
        <button type="button" onClick={() => signIn}>로그인</button>
    )
  }

}
```

</div>
</details>

---

<details>
<summary>

## 2주차 - 금요일

</summary>
<div>

## [ 헤딩 레벨(Heading Level) ]

- 크롬 익스텐션 : tota11y

```
- 웹 페이지 접근성에 대한 정보 제공
- 접근성이 지켜지지 않는 부분에 대해서 경고 메세지 제공
```

- 라이브러리 : tenon-io/tenon-ui

```
import { Heading } from '@tenon-io/tenon-ui'

// 레벨1
<Heading.H>최상단 레벨</Heading.H>

<Heading.LevelBoundary>
  // 레벨2
  <Heading.H>상단 레벨</Heading.H>
  <Heading.LevelBoundary>
    // 레벨3
   <Heading.H>하위 레벨</Heading.H>
  </Heading.LevelBoundary>
</Heading.LevelBoundary>
</Heading.H>
```

## [ 히든 콘텐츠(Hidden Contents) ]

- a11yHidden style example : 화면상으로 보이지는 않지만, 스크린리더로 접근 가능하도록

```
overflow: hidden;
position: absolute;
clip: rect(0, 0, 0, 0);
width: 1px; // for Screen Reader
height: 1px;
margin: -1px;
border: 0;
padding: 0;
```

- React를 사용한다면 class 속성으로 style을 적용해도 되지만, 컴포넌트화 하는 것도 방법이다.

## [ 버튼 컴포넌트(Button Component) ]

```
- 버튼의 기능을 하는 요소는 <div>, <img> 요소와 같은 포커스로 접근이 안 되는 컨텐츠를 사용해서는 안 된다.(스크린리더에서 접근 불가)

- 스크린리더에서 버튼에 접근했을 때, 버튼의 역할, 컨텐츠 정보 등을 제공해야 한다
```

## [ 사용에 주의가 필요한 HTML 표준 문법 ]

```
- <li>요소는 오직 <ol>,<ul>요소의 자식요소로써 사용할 수 있다

- <caption>요소를 <table>요소의 첫번째 자식요소로 배치해야 한다.

- <figcaption>요소는 오직 <figure>요소의 자식요소로써 사용할 수 있다.
```

## [ 접근성 자동 검사 (React-axe) ]

- 라이브러리 : react-axe

```
$ npm i -D react-axe
```

예제

```
import React from 'react'
import ReactDOM from 'react-dom'
import axe from 'react-axe'

// 개발환경에서 확인 후 수정해야 하므로 배포환경이 아닌 경우 동작하도록 설정
if (process.env.NODE_ENV !== 'production') {
  axe(React, ReactDOM, 1000)
}

ReactDOM.render(<App />, document.getElementById('root'));
```

</div>
</details>

---

<details>
<summary>

## 3주차 - 월요일

</summary>
<div>

### [ 시작하기 ]

- cra-template-ko-craco 커스텀 템플릿을 사용하여 프로젝트 시작하기

### [ 문서 헤드 구성 ]

- .env (환경 변수 파일)

```
- 환경 변수란? 특정 프로세스를 위한 '키=값' 형태의 변수를 말한다.
```

- og (open graph)

```
- 오픈 그래프 프로토콜? 페이스북에서 처음 만들어졌으며, 웹사이트의 메타 데이터를 표기하는 방법 중 하나
- 공유 된 링크 사이트의 '미리보기' 정보를 제공한다.(제목, 설명, 이미지 등등...)
- 트위터는 자체적인 메타데이터 표기법을 사용하고 있음
- 코드상 메타 데이터 값을 수정했다하더라도, 애플리케이션에서 캐싱된 데이터를 참조할 수 있기때문에 변경이 되지 않은 것처럼 보일 수 있다(이는 캐시가 소멸되거나, 캐싱을 리로드 시켜야 한다)

<meta property="og:lang" content="ko-KR" />
<meta property="og:title" content="이디야(Ediya) UI ← React 실습" />
<meta property="twitter:title" content="이디야(Ediya) UI ← React 실습" />
<meta
  property="og:description"
  content="이듬 블렌디드 러닝 '이디야(Ediya) UI ← React 실습' 시연으로 제작한 결과물입니다."
/>
<meta property="og:image" content="%PUBLIC_URL%/assets/og-image.jpg" />
```

### [ 컴포넌트 디렉토리 구성 ]

- components, api 디렉토리 구성

### [ 컴포넌트 구성 Part 1 ]

- 동적으로 모듈 import()

```
- 필요에 따라 모듈을 import 할 수 있다
- 함수형 구문인 import()는 promise()를 반환한다.
- 계산된 모듈 이름을 사용할 수 있다

const modulePage = 'page.js';
import(modulePage)
  .then((module) => {
    module.default();
  });
```

예제

```
// 작업 환경이 '배포'환경 일 때, 모듈을 불러와서 사용하도록 설정
// '배포'환경이 아닌 경우에는 해당 모듈을 import 하지 않는다
if (process.env.NODE_ENV === 'production') {
  import('~/config/serviceWorker')
    .then(serviceWorker => serviceWorker.register)
    .catch(error => console.error(error.message))
}
```

- import 파일 경로 설정

```
import { AppHeader } from "~/components/AppHeader/AppHeader"

위와 같이 파일 경로에 '~'와 같은 임의의 경로를 사용하고 싶을 경우
jsconfig.json에서 해당 경로를 설정해 주면 된다.
```

예제

```
// jsconfig.json
{
  compilerOptions: {
    "baseUrl": "src",
    "paths": {
      "~/*": [
        "./*"
      ],
      ...
    }
  }
}
```

### [ 컴포넌트 구성 Part 2 ]

- AppHomeLink, AppNavigation, BeverageList, BeverageItem 컴포넌트
- 컴포넌트 스타일 관리

### [ 컴포넌트 props 디자인 ]

- '나머지 매개변수'와 '구조 분해 할당'을 사용한 props 바인딩
- 동적으로 컴포넌트 태그 설정하기

```
import { SubComponent } from './SubComponent.js'

<SubComponent
  // 상위 컴포넌트에서 props 전달하기
  wrapperProps={
    {
      as: 'h2',
      title: '래퍼'
      className: 'wrapper'
    }
  }
  href="/"
  className="content"
  title="컨텐츠"
  external>
  <p>이것도 같이 전달해줄게</p>
</SubComponent>
```

```
// SubComponent.js

const SubComponent = ({
  // 구조 분해 할당과 나머지 매개변수 활용
  // wrapperProps.as의 경우 별칭을 사용하였으며, TitleCase를 사용한 이유는 기존의 태그와 구분을 해야 하므로
  wrapperProps: {as: WrapperComponent, wrapperClassName, href, title, ...restWrapperProps},
  className,
  ...restContentProps
}) => {
  // 컴포넌트의 tag를 동적으로 설정(wrapperProps.as로 설정한 값으로 태그를 설정할 수 있다)
  <WrapperComponent
    ...restWrapperProps
    className={wrapperClassName}
  >
    <a
      {...restContentProps}
      className={className}
      href={href}
      title={title}
      target={external ? "_blank" : null}
      rel={external ? "noopenner noreferrer" : null}>
      <span className="a11yHidden" lang="en">
        EDIYA COFFEE
      </span>
    </a>
  </WrapperComponent>
}
```

- 전달 받은 props에 대한 기본값 설정하기

```
방법 1 - 바인딩 할 때, 조건처리

<a
  {...restContentProps}
  className={className || ''}
  href={href || '/'}
  title={title || '링크'}
  target={external ? "_blank" : null}
  rel={external ? "noopenner noreferrer" : null}>
  <span className="a11yHidden" lang="en">
    EDIYA COFFEE
  </span>
</a>
```

```
방법 2 - defaultProps 사용하기

SubComponent.defaultProps = {
  wrapperProps: {
    as: 'h1',
    title: 'wrapper'
  },
  title: 'content',
  href: '/'
}
```

[ 질문 ]

- 오프라인 수업에서 나머지 매개변수로 설정한 속성들을, 속성 중 가장 먼저 선언해야 한다고 하셨는데 무슨 이유였죠?

</div>
</details>

---

<details>
<summary>

## 3주차 - 화요일

</summary>
<div>

### [ AppNavigation 컴포넌트 이벤트 핸들링, 타임 컨트롤 ]

컨텐츠가 상태에 따라 show/hide 되는 경우 style 뿐만 아니라 hidden 속성도 같이 적용해줘야 한다.

```
-> hide style을 어떻게 적용했는지에 따라, 화면에 보이지 않을지라도 스크린리더에서 접근이 가능한 경우가 있다
-> 이러한 문제점을 방지하기 위해 컨텐츠를 hide 할 경우 hidden 속성도 같이 toggle 해 주어야 한다
```

### [ Context API → AppNavigation 리스트 렌더링 ]

- 컴포넌트의 props 설정 값은 해당 컴포넌트의 최상위 wrapper 컴포넌트의 속성으로 자동 적용됨.
- 전달한 속성과 컴포넌트 내부에 작업된 속성이 중복될 경우 나중에 선언된 것이 적용된다.

```
import SubComponent from './component/SubComponent.js'

<SubComponent id="전달한 아이디" title="전달한 타이틀" onClick="전달한 이벤트">
  ...
</SubComponent>
```

```
// SubComponent.js

export const SubComponent = () => {
  <button id="내부 아이디" type="button">
    버튼
  </button>
}
```

```
// 렌더링 된 실제 SubComponent

<button type="button" id="전달한 아이디" title="전달한 타이틀" onClick="전달한 이벤트">
  버튼
</button>
```

### [ 키보드 접근성 (ref, forwardRef, shouldComponentUpdate) 설정 ]

- 컨텐츠 show/hide 여부에 따라 불필요한 이벤트가 있을 경우에는 해당 이벤트를 제거해줘야 한다 (이 때, 해당 이벤트는 별도의 함수로 작업해야 함)

- ref는 사용을 자제해야 하며, 사용해야 하는 경우는 다음과 같다

```
1. 포커스, 텍스트 선택 영역, 미디어 재생 관리
2. 3rd Party 라이브러리 활용
3. 애니메이션 직접 처리

ref를 사용하기 전에 state를 사용하여 작업할 수 있는지, 또는 props와 callback 함수를 사용하여 구현할 수 있는지 고민해볼것
```

### [ 컴포넌트 참조 전달(forwardRef)과 개발 도구에서 이름 표시 설정 ]

- 학습 완료

[ 질문 ]

질문1) React.createContext(initValue)에서 초기값(initValue)으로 설정한 값은 사용할 수 없는건가요?

```
// 초기값 설정
const initValue = "hello react"
// 컨텍스트 생성
const MyContext = React.createContext(initValue)
```

제가 예상한 초기값 설정시 컨텍스트 작업

```
// 초기값을 설정했으므로 value를 따로 건네주지 않음
<MyContext.Provider>
  <App />
</MyContext.Provider>


<MyContext.Consumer>
  {
    (value) => {
      console.log(value) // undefined
    }
  }
</MyContext.Consumer>
```

제대로 동작하는 경우

```
// 정상 동작 : value로 initValue 건네줌
<MyContext.Provider value="initValue">
  <App />
</MyContext.Provider>

<MyContext.Consumer>
  {
    (value) => {
      console.log(value) // "hello react"
    }
  }
</MyContext.Consumer>
```

질문2) 학습 내용 질문은 아니고 강사님에게 조언을 듣고 싶은데, 이번에 미니 프로젝트를 따라 해보면서 느낀게 확실히 컨텐츠를 구현해보는게
부족한 부분이 어딘지 알고, 어려웠던 내용이 보다 이해가 잘 되고 기억에 잘 남는것 같습니다. 그래서 강의 예제 코드 이외에 어느정도 규모있는 토이프로젝트를 진행하면서 그 때 그 때 조금씩 배운 내용들을 적용해보고 싶은데, 지금보다 이론 학습 이후에 전체적인 내용을 학습하고 프로젝트를 만드는게 더 나을까요? 만약 프로젝트를 진행한다면 따라해보기에 추천해주실만한 사이트나 오픈 API가 있을까요~?? 나중에 답변주셔도 됩니다 :)

</div>
</details>

---

<details>
<summary>

## 3주차 - 수요일

</summary>
<div>

### [ React 훅(Hook) ]

#### useState() 훅을 활용한 상태 관리

```
- 훅(Hook)을 사용하면 함수형 컴포넌트에서도 클래스 컴포넌트에서만 사용할 수 있었던 state 등의 여러 리액트 기능을 사용할 수 있다.

- 훅(Hook)을 사용할 때는 반드시 다음 규칙에 따라야 한다
  1. React 함수형 컴포넌트 안에서만 사용
  2. 컴포넌트 안의 반복문 | 조건문 | 중첩된 함수 안에서 훅을 사용해서는 안 된다.
```

#### React 클래스 컴포넌트 → 함수형 컴포넌트로 전환 (상태 관리)

학습 완료

#### useEffect() 훅을 활용한 사이드 이펙트 처리

- useEffect(fn [, target])

```
- 함수형 컴포넌트의 useEffect() 훅은 라이프 사이클 훅을 하나의 API로 통합한 것이다.
- useEffect()는 전달 받은 함수를 'DOM 업데이트 이후 시점'에 실행
- 설정된 함수는 '컴포넌트 내부'에 위치해 있어서 state, props에 접근 가능하다.
- 컴포넌트 렌더링, 업데이트 이후 시점(componentDidMount, componentDidUpdae)에 빠짐없이 실행된다.
```

기본 예제

```
import React, {useEffect} from 'react'

function CountDown (props) {
  useEffect(()=>{
    ...
  })
}
```

컴포넌트 제거 이전 시점에서 코드 실행이 필요한 경우

```
useEffect(() => {
  ...
  return () => {
    컴포넌트 제거 되기 전(componentWillUnmount)에 실행됨.
  }
})
```

useEffect의 성능 이슈(모든 상태 변화에 반응하므로, 필요한 상태의 변화에만 실행되도록 설정하는 것이 좋다)

```
userEffect(() => {
  ...
}, [targetState])
```

#### useRef() 훅을 활용한 DOM 노드 접근/조작

- useRef() 훅은 실제 DOM 노드를 참조(Ref.)할 경우에 사용된다.
- 실제 DOM을 참조하는 것이기 때문에 컴포넌트 '라이프 사이클 훅'과는 관련이 없다.(컴포넌트가 다시 렌더링 되지 않는다)

#### useContext() 훅을 활용한 데이터 공유

```
import React, {useContext} from 'react'
import AuthContext from '../context/AuthContext'


function SingIn (props) {
  const authContext = useContext(AuthContext)
  const { isAuth, signIn} = authContext
  return (
    {
      isAuth ?
        <div>...</div> :
        <button onClick={()=>{signIn}}>...</button>
    }
  )
}
```

### [ 리스트 렌더링 & 컨텍스트 Part 2 ]

실습 완료

### [ 페이지 상단 스크롤 이동 ]

실습 완료

</div>
</details>
