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

## JSX
- babel 사용 `<script type="text/babel">`
- `JSX` : JS + XML
- (html이 아니라 xml이기 때문에 싱글 태그도 닫는 태그를 꼭 넣어주어야함)
- babel의 역할 = `createElement` -> `<>`
- 컴포넌트는 대문자로 시작, 태그는 소문자
- `<></>` : 최상단에 들어가는 껍데기(div대신)
- DOM에 직접 접근하고 싶을때는 `ref`사용
```
ref={(c) => {this.input = c; }} 
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
- setState가 실행될 때 마다 render가 실행됨(따라서 따로 뺄 수 있는건 빼주는게 좋음)
