[웹 게임을 만들며 배우는 React - 조현영님](https://inf.run/WKgp)  

## React를 쓰는 이유
- 웹에서 앱과 같은 사용자 경험을 만들어줌
- 데이터 처리(싱크로나이즈)
- 컴포넌트 재사용

## React
> React, react-dom
- 컴포넌트들을 렌더링할 루트(div)가 필요
- 상태(state) = 바뀌는, 바뀔여지가 있는 부분
- 클래스 사용 시 클래스1 === 컴포넌트1
- `class` 대신 `className` `For` 대신 `htmlFor` html과 헷갈릴 수 있어서 구분

## JSX
- babel 사용 `<script type="text/babel">`
- `JSX` : JS + XML
- (html이 아니라 xml이기 때문에 싱글 태그도 닫는 태그를 꼭 넣어주어야함)
- babel의 역할 = `createElement` -> `<>`
- 컴포넌트는 대문자로 시작, 태그는 소문자
- `<></>` : 최상단에 들어가는 껍데기(div대신)
- `value`와 `onChange`는 세트(or `defaultValue`)

# Class
- DOM에 직접 접근하고 싶을때는 `ref`사용
```
input;
...
render() {
    return (
        <input
            ref={(c) => {this.input = c; }} 
        />
    )
}
```

## setState
- 예전 값으로 새로운 state를 만들때는 함수 사용
```
this.setState((prevState) => {
    return {
        result: prevState.value + '정답',
        first: Math.ceil(Math.random() * 9 ),
        second: Math.ceil(Math.random() * 9 ),
        value: '',
    };
});
```
- setState는 비동기
- setState가 실행될 때 마다 render만 같이 실행됨(따라서 따로 뺄 수 있는건 빼주는게 좋음)


# React Hooks
- 함수 컴포넌트 : setState나 ref를 안쓰는 경우에 썼었음
- Hooks = 함수 컴포넌트 + state, ref ...
- setState 분리
```
const GuGuDan = () => {
    const [first, setFirst] = React.useState(Math.ceil(Math.random() * 9 ));
    const [second, setSecond] = React.useState(Math.ceil(Math.random() * 9 ));
    const [value, setValue] = React.useState('');
    const [result, setResult] = React.useState('');
}
```
- state가 바뀔 때 마다 함수가 다시 실행되므로 느릴 수 있음(렌더링)
- setState는 비동기이기 때문에 모아서 한번에 처리됨


## 웹팩
- 스크립트의 중복을 최소화 하기 위해 웹팩 등장
- node.js는 자바스크립트(웹팩) 실행기
- **웹팩 셋팅**
- `npm init` - `npm i react react-dom` - `npm i -D webpack webpack-cli`
- `webpack.config.js` 
- 플러그인들의 모음이 프리셋
- [browserslist](https://github.com/browserslist/browserslist)
```
const path = require('path');

module.exports = {
    name: 'wordrelay-setting',
    mode: 'development', // 실서비스 : production
    devtool: 'eval',
    resolve: {
        extensions: ['.js', '.jsx'],
    },
    entry: {
        app: ['./client'],
    }, // 입력(불러오는 파일은 같이 입력됨)
    module: {
        rules: {
            test: /\.jsx?/,
            loader: 'babel-loader',
            options: {
                presets:[
                    ['@babel/preset-env', {
                        targets: {
                            browsers: ['> 1% in KR'], // 지원 브라우저 지정가능
                        },
                        debug: true,
                    }], 
                    '@babel/preset-react'
                ],
                plugins: [''],
            },
        },
    },
    plugins: [],
    output: {
        path: path.join(__dirname, 'dist'),
        filename: 'app.js',
    }, // 출력
};

```
- `client.jsx`
    ```
    const React = require('react');
    const ReactDom = require('react-dom');
    const WordRelay = require('./WordRelay');

    ReactDom.render(<WordRelay />, document.querySelector('#root'));
    ```
- `index.html`
    ```
    <div id="root"></div>
    <script src="./dist/app.js"></script>
    ```
- 클래스(컴포넌트) jsx로 쪼개기
- **웹팩 실행**
    1. package.json - script
    2. npx webpack


## react-refresh
- 핫 리로딩 기능, 변경사항을 감지해서 반영해줌.
    - 리로딩과는 다름(리로딩은 새로고침으로 데이터가 날아감)
```
"dev": "webpack serve --env development"
// script 서버실행

"react-refresh": "^0.11.0",
"@pmmmwh/react-refresh-webpack-plugin": "^0.5.4",
"webpack-dev-server": "^4.7.4"
//설치
```
- 추후 webpack.config.js 링크[]()


## map
- 리액트에서의 반복문
- key값은 고유해야함(i는 쓰면 안됨)
```
{[
    { fruit:'사과', taste:'맛있다' },
    { fruit:'사과', taste:'맛없다' }
].map((v, i) => {
    return (
        <li key={v.fruit + v.taste}><b>{i + v.fruit}</b> - {v.taste}</li>
    );
})}
```

## props
[props 공식문서](https://ko.reactjs.org/docs/components-and-props.html)


## React 성능향상
- React DavTools
- `class` 사용 시 `shouldComponentUpdate(nextProps, nextState, nextContext)`
    - true면 렌더링, false면 렌더링X
    - 렌더링 타이밍을 선택할 수 있음
- `class` 사용 시 `PureComponent` 사용
- `hooks` 사용 시 `React.memo` 사용
    - 컴포넌트를 `memo()`로 감싸줌
- 자식컴포넌트가 모두 `PureConponent` or `memo()`면 부모도 적용 가능
- `props`는 부모가 바꿔야함. 자식X
    - 바꿔야 한다면 자식 컴포넌트에서 `props`를 `state`에 넣어줌
- `jsx`안에서는 `for, if` 사용 불가
    - 삼항연산자로 작성
- `hooks`에서는 `this`의 속성들을 `Ref`로 표현
- 비동기함수에서 바깥쪽 변수를 참조하면 클로저 발생
- `useMemo` : 복잡한 함수 결과값을 기억
- `useCallback` : 함수 자체를 기억
    - 함수 자체의 생성이 너무 오래 걸릴 경우 기억
- `useRef` : 일반 값을 기억


## state와 ref의 차이
- `state`는 set하게 되면(바뀌면) 다시 렌더링
- `ref`는 바뀌어도 렌더링 되지 않음
    - `ref`는 항상 `ref.current`로 접근


## 라이프사이클 LifeCycle
#### Class
- `componentDidMount()` : 처음 컴포넌트 렌더가 성공적으로 실행된 직후 (비동기요청을 많이함)
- `componentWillUnmount()` : 컴포넌트가 제거되기 직전 (비동기요청 정리)
    - 위 두가지가 보통 쌍으로
- `componentDidUpdate()` : 리렌더링 후
#### hooks
- `useEffect()` : 두번째 인자에 들어가는 값이 바뀔 때마다 함수 내용이 다시 실행됨
    - 아무런 값도 안들어가면 맨 처음에만 실행되고 다시 실행되지 않음
    - `useEffct`를 여러번 쓸 수도 있음
```
useEffect(() => { // componentDidMount, componentWillUnmount 역할(1대1 대응은 아님)
    return () => { // componentWillUnmount 역할
        
    }
}, []) // closer 해결(배열에 넣은 값들이 바뀔때 useEffect가 실행)
```


## useReducer (hooks)
- `state`는 직접 변경 불가능
    - 이벤트 발생을 통해 `action`을 `dispatch`해서 변경
    - 어떻게 바꾸는지는 `reducer`에 기록
```
const initialState = {
    winner: '',
    turn: 'O',
};

const SET_WINNER = 'SET_WINNER';

const reducer = (state, action) => {
    switch (action.type) {
        case SET_WINNER:
            return {
                ...state, // 기존 state 얕은 복사
                winner: action.winner,
            }
    }
};
.
.
.
    const onClickTable = useCallback(() => {
        dispatch({ type: SET_WINNER, winner: 'O' }); // action 객체를 dispatch
    }, []);
```