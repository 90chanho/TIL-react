# TIL

### [프리페어링 학습]

- Github 저장소 생성(repository name : TIL-react)
- Git Kraken 설치 & GitHub 저장소 클론
- GitHub 저장소에 변경 사항 커밋 후 푸시

---

## 1주차 - 월요일 학습

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

---

## 1주차 - 화요일 학습

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

---

## 1주차 - 수요일

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

### [ 미숙한 ES6 학습  - Promise ]
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
