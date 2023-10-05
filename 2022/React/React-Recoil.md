# Recoil

[공식문서](https://recoiljs.org/ko/docs/introduction/getting-started/)

## 개요

- Atom에 value를 넣고 필요한 component가 접근해서 사용하거나 수정함
- Traveling Prop을 해결함

## RecoilRoot

- recoil 상태를 사용하는 컴포넌트는 부모 트리에 `RecoilRoot`가 필요하므로 루트 컴포넌트에 `RecoilRoot`를 넣어줌

## Atom

- **Atom**은 **상태(State)**의 일부를 나타냄
- Atoms는 어느 컴포넌트에서나 읽고 쓸 수 있음
- Atom에 어떤 변화가 있으면 그 Atom을 구독하는 모든 컴포넌트들이 재 랜더링 됨

```
// atoms.ts

export const textstate = atom({
  key: "textState",
  // unique ID (with respect to other atoms/selectors)
  default: "",
  // default value (aka initial value)
})
```

- 컴포넌트에서 atom을 읽고 쓰기 위해서 아래와 같은 Hook을 사용할 수 있음

## Hooks

- `useRecoilValue(Atom)` : Atom의 값을 반환
- `useSetRecoilState(Atom)` : Modifier를 반환
- `useRecoilState(Atom)` : 값과 Modifier를 반환(setState와 같음)

```
...
function TextInput() {
  const [text, setText] = useRecoilState(textState);

  const onChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={onChange} />
      <br />
      Echo: {text}
    </div>
  );
}
```

## Selector

- **Selector**는 파생된 상태(**derived state**)의 일부를 나타냄
- 파생된 상태 === 상태의 변화
- `useRecoilValue(selector)` hook을 사용해서 값을 읽을 수 있음

```
// atoms.ts

export const hourSelector = selector<number>({
  key: "hours",
  get: ({ get }) => {
    const minutes = get(minuteState);
    return minutes / 60;
  },
  set: ({ set }, newValue) => {
    const minutes = Number(newValue) * 60;
    set(minuteState, minutes);
  },
});
```
