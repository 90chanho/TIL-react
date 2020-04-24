# 오프라인 강의

## 오프라인 강의 1일차

### 이론?

- npm i 보다 npx 사용을 권장
- 업데이트를 할 때에는 툴 체인을 사용?

[ 리액트 프로젝트 템플릿 ]

```
// 기본형 템플릿 적용
npx create-react-app

// 특정 템플릿 적용
npx create-react-app <project-name> --template cra-template-
```

- 내부

```
cra-template
cra-template-typescript
```

- 외부
  npm 사이트에서 검색하면 많아

```
cra-template-*
```

- 커스텀 템플릿도 생성 가능

[ poly-fill ]
IE 9 ~ 11까지 지원하도록

```
npm i react-app-polyfill
```

적용 방법

```
// 엔트리 JS 파일 최상단에서 적용해야 함
import 'react-app-polyfill/ie9'
```

[ 브라우저 호환 ]

### 실습

- 라이브러리 : classNames

```
기존 클래스에 props로 전달받은 class 추가하기
```

- 전개연산자를 이용한 요소 attribute 적용하기

```
매개변수에서 나머지 매개변수 사용하고
해당 요소에서 전개연산자로 적용
```

- eslint에서 문제 없는 부분 검사 대상에서 제외하기

```
// 파일 최상단에서 해당 내용 입력 : 해당 파일에서 전체 적용
/* eslint-disable jsx-a11y/anchor-is-valid */
```

- 표준 태그를 사용할 것인지 aria-role을 사용할 것인지 선택해야 한다면 '표준 태그'가 우선이다
