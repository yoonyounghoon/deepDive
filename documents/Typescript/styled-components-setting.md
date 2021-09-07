# typescript & styled-components 세팅 
<hr/>
## styled.d.ts 파일 작성

```jsx
// styled-components의 타입정의를 불러와 내가 사용할 신규 타입정의 추가 & 확장
// global style type 작성
import 'styled-components';

declare module 'styled-components' {
  // 1. 인터페이스 지정
  export interface 인터페이스명지정 {
    속성1 : 타입지정;
  }
  // 2. 타입속성지정
  export type 타입명 = {
    속성1 : 타입지정;
  }
  export interface DefaultTheme {
        mainBackground: string,
        textColor: string

   }
}
```

## 많이 사용하는 css 변수 등록하는 theme 파일 작성

```jsx
// 많이 사용하는 글로벌 css를 변수로 작성하는 theme 작성

import { DefaultTheme } from "styled-components";

const theme: DefaultTheme = {
    mainBackground: '#fff',
    textColor: '#292B2E'
}

export default theme;
```

## 스타일 적용

```jsx
import React from 'react';
import styled, { ThemeProvider } from 'styled-components';
import theme from './styles/theme';

const Container = styled.div`
  background-color: ${(props) => props.theme.mainBackground};
  color: ${(props) => props.theme.textColor};
`;

function App() {
  return (
    <ThemeProvider theme={theme}>
      <Container>
        <h1>테마 적용하기</h1>
      </Container>
    </ThemeProvider>
  );
}

export default App;
```

## 스타일 작성하기

### 1. 단일 props 사용시

```jsx
// styled-components에 1개 props 타입지정
// const Container = styled.div< {프롭스명 : 타입지정} >`
const Container = styled.div< { age : number } >`
  color: ${(props) => (props.age > 20 ? 'red' : 'gray')};
`;
```

### 2. 다수 props 사용시: interface 사용

- 인터페이스로 분리하여 타입지정하는것 뿐 이외에 사용법은 동일

```jsx
// Container styled-components에 적용할 interfacer를 작성
interface Container extends 상속타입 {
  isActive: boolean;
  age: number;
  프롭스명: 타입지정;
}
// styled-components에 interface 타입 지정하기
const Container = styled.div<Container>`
  color: ${(props) => (props.age > 20 ? 'red' : 'gray')};
  background-color: ${(props) => (props.isActive ? 'red' : 'gray')};
`;
```