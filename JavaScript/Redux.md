# Vanilla Redux

[공식문서](https://ko.redux.js.org/introduction/getting-started/)

- Redux는 `JavaScript Apps`를 위한 상태관리 라이브러리(React에 의존하지 않음)
- **Mutating(변경) State XXX, return new State Objects OOO**

## Store and Reducer

- 데이터(state)를 넣는 곳
- `createStore(reducer)` : store는 reducer를 요구함
- `reducer` : data를 modify하는 function, return data
  - data를 변경할 수 있는 유일한 곳
  ```
  const countModifier = (state = 0) => {
    return state;
  };
  // state가 initial되지 않으면 undefined를 반환
  // state = 0 은 맨 처음 data를 initial하는 것
  // state는 currentState
  ```
- `store.getState()` : return하는 data를 가져옴

## Actions

- `action` : redux에서 function을 부를 때 쓰는 두번째 parameter or argument
- `reducer`와 소통하기 위한 방법
- `store.dispatch({key: value})`

```
const countModifier = (count = 0, action) => {
  switch (action.type) {
    case PLUS:
      return count + 1;
    case MINUS:
      return count - 1;
    default:
      return count;
  }
};

store.dispatch({ type: "PLUS" });
```

## Dispatch

```
// action만 return하는 function을 따로 만들어서 사용
const addToDo = (text) => {
  return { type: ADD_TODO, text, id: Date.now() };
};

const deleteToDo = (id) => {
  return { type: DELETE_TODO, id };
};

...

const dispatchAddToDo = (text) => {
  store.dispatch(addToDo(text));
};

const dispatchDeleteToDo = (event) => {
  const id = parseInt(event.target.parentNode.id);
  store.dispatch(deleteToDo(id));
};
```

## Subscribe

- store안에 있는 변화를 감지
- `store.subscribe(function)`

```
const onChange = () => {
  number.innerText = countStore.getState();
};

countStore.subscribe(onChange);
```

# React Redux

[공식문서](https://react-redux.js.org/introduction/getting-started)

```
<Provider store={store}>
  <App />
</Provider>
```

## Hooks를 이용하는 방법

[공식문서](https://react-redux.js.org/api/hooks)

- `useSelector()` => `mapStateToProps()` => `store.getState()` : 상태 조회하기
- 조회할 때는 꼭 필요한 필드만 가져오기(store에서 수정되면 참조하는 모든 컴포넌트가 리렌더링 되기 때문)
- 최적화 방법

  - 독립 선언(여러번 사용)
  - equalityFn 사용하여 이전값이랑 달라졌을 경우에만 리렌더
  - shallowEqual 함수

  ```
  ...
  const toDos = useSelector((state) => state.toDos);
  ...
  ```

- `useDispatch()` => `mapDispatchToProps()` => `store.dispatch()` : Action Dispatch하기
- hook 자체가 dispatch, 내부 인자로 action 객체를 받음
- 컴포넌트가 리렌더링 될때마다 함수가 새로 만들어지는 것을 방지하도록 useCallback과 함께 사용하기
  ```
  ...
  const dispatch = useDispatch();
  const addToDo = useCallback(() => dispatch(add()), [dispatch]);
  ...
  ```

## connect 함수를 이용하는 방법

- 고차 컴포넌트(HOC) connect()를 이용하는 방법
- 더 이상 권장하지 않음
- `mapStateToProps()` : `store.getState()`

  ```
  ...
  const mapStateToProps = (state) => {
    return { toDos: state };
  };

  export default connect(mapStateToProps)(Home);

  ```

- `mapDispatchToProps()` : `store.dispatch()`

  ```
  ...
  const mapDispatchToProps = (dispatch) => {
    return { addToDo: (text) => dispatch(actionCreators.addToDo(text))};
  };

  export default connect(mapStateToProps, mapDispatchToProps)(Home);`
  ```

# Redux Toolkit

[공식문서](https://redux-toolkit.js.org/introduction/getting-started)
