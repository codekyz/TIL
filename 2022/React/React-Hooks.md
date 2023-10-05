# React Hooks

- 함수형 컴포넌트에 State를 줌(hooks는 react의 state machine에 연결하는 기본적인 방법)
- 함수형 프로그래밍 스타일
- 클래스 컴포넌트에 비해 짧은 코드(this와 같은 규칙없음)
- 이해하기 쉽고 직관적

# useState

- `const [value, modifierValue] = setState();`
- Array를 리턴함
- modifier는 re-render함

# useInput(custom hook)

```
const useInput = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: { value }
    } = event;
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(value);
    }
    if (willUpdate) {
      setValue(value);
    }
  };
  return { value, onChange };
};
```

# useEffect

[공식문서](https://ko.reactjs.org/docs/hooks-effect.html)

- componentDidMount, componentDidUpdate, componentWillUnmount의 기능을 하는 hook
- 두번째 인자로 dependency를 받고 dependency가 업데이트 되는지에 따라서 첫번째 인자로 받은 function이 실행됨
- CleanUp function(return function)으로 componentWillUnmount 역할을 함

# useContext

[공식문서](https://ko.reactjs.org/docs/hooks-reference.html#usecontext)

- `const value = useContext(MyContext);`
- context 객체(React.createContext)를 받아 그 context의 현재 값을 반환
- context의 현재 값은 트리 안에서 해당 Hook을 호출한 컴포넌트에서 가장 가까이 있는 `<MyContext.Provider value={value}>` 에 의해 결정
- useContext를 호출한 컴포넌트는 context값이 변경되면 항상 리렌더링 됨(memoization을 사용해 최적화)

# useRef

[공식문서](https://ko.reactjs.org/docs/hooks-reference.html#useref)

- reference는 기본적으로 components의 어떤 부분을 선택할 수 있는 방법

# React Lifecycle

[React Lifecycle](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

- 각각의 컴포넌트는 라이프사이클(생명주기)를 가짐
- 크게 세가지 상태로 나눌 수 있음 **생성될때(마운트) / 업데이트할때(state가 바뀔 때 / props가 바뀔 때 / 부모 컴포넌트가 리렌더링될 때) / 제거할때(언마운트)**

## Render 단계

- constructor : 클래스형에서 초기 state를 정할 때 사용
- useState : hooks에서 초기 state를 정할 때 사용

- shouldComponentUpdate : 클래스형에서 props나 state를 변경했을 때 리렌더링 할지 말지 결정하는 메서드(성능을 위해서는 PureComponent사용을 추천)
- React.memo / useMemo : hooks에서 렌더링 성능을 개선할 때 사용

- render : 컴포넌트를 렌더링할 때 필요한 유일한 필수 메서드(hooks에서는 필요없음, 함수 컴포넌트 본체 자체)

## Commit 단계

- DOM을 사용하여 부수효과를 실행하고 업데이트를 예약
- React DOM 및 refs 업데이트

- componentDidMount : 컴포넌트를 만들고 첫 렌더링을 마친 후 실행
- useEffect : hooks에서 위의 기능을 구현하기 위해 사용

- componentsDidUpdate : 리렌더링이 완료된 후 실행

- componentsWillUnmount : 컴포넌트를 DOM에서 제거할 때 실행
- useEffect CleanUp function : hooks에서 위의 기능을 구현하기 위해 사용
