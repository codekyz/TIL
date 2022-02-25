# styled-components

[노마드코더 - React JS 마스터 클래스](https://nomadcoders.co/react-masterclass/lobby)  
[https://styled-components.com/](https://styled-components.com/)

## Install

- `CRA` 후에
- `npm i styled-components`

## Using

### 1. import

```
import styled from "styled-components";
```

### 2. Create styled components

- `백틱` 사이에는 `css`가 들어감
- vscode 익스텐션 설치하면 자동완성
- 클래스 네임은 랜덤하게 지정됨

```
const Father = styled.div`
  display: flex;
`;

const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;
}
```

### 3. Adapting and Extending

- adapting(modify)
- `props` 사용 가능

```
const Box = styled.div`
  background-color: ${(props) => props.bgColor}
`;

...중략

  <Box bgColor="tomato" />
```

- extending
- `styled(기존컴포넌트)`
- 기존 컴포넌트의 모든 속성에 새로운 속성을 더 해줌

```
const Circle = styled(Box)`
  border-radius: 50px;
`;

...중략

<Circle bgColor="teal" />
```

### 4. 'As' and Attrs

- `as`라는 props를 이용하면 정의된 스타일을 그대로 가지고 가되 태그네임을 바꿀 수 있음

```
const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;

...중략

  <Btn>Log In</Btn>
  <Btn as="a" href="#">
    Link
  </Btn>
```

- `attrs` 를 이용하면 html의 속성을 미리 설정할 수 있음
- 여러개에 동일한 설정이 필요할 경우 유용

```
const Input = styled.input.attrs({ required: true, minLength: 10 })`
  background-color: tomato;
`;
```

### 5. Animations and Pseudo Selectors

- animations
- `keyframes`라는 헬퍼 함수를 추가
- 밖에서 animation을 선언하고 `styled-components`안에서 사용

```
import styled, { keyframes } from "styled-components";

const rotate = keyframes`
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
`;

const Box = styled.div`
  width: 200px;
  height: 200px;
  background-color: tomato;
  animation: ${rotate} 1s linear infinite;
`;
```

- seudo Selectors
- `styled-components`가 아니더라도 컴포넌트 내에서 하위 태그에 대한 타겟 선택 가능
- 축약어 `&`
- case1

```
const Box = styled.div`
  ...중략
  span {
    font-size: 36px;
    &:hover {
      font-size: 40px;
    }
  }
`;

...중략

  <Box>
    <span>🤗</span>
  </Box>

```

- `styled-components` 내에서 하위 컴포넌트에 대한 타겟 선택 가능(변수명처럼 사용)
- case2

```

const Emoji = styled.span`
  font-size: 36px;
`;

const Box = styled.div`
  ...중략
  ${Emoji}:hover {
      font-size: 98px;
  }
`;

...중략

  <Box>
    <Emoji as="p">🤗</Emoji>
  </Box>

```

### Themes

- 모든 색상을 가지고 있는 object
- index.js에서 설정하고 App.js에서 `props`로 가져다 씀
- [공식문서](https://styled-components.com/docs/advanced)
- _완전 쿨함🤩_
