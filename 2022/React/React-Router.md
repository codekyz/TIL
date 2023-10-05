# React Router

> react-router-dom ver.6

[공식문서](https://reactrouter.com/docs/en/v6/getting-started/overview)

## Installation

```
npm i react-router-dom
```

## Configuring Routes

- v6로 바뀌면서 `switch`는 `Routes`로 대체되었음
- `<Route><Route/>` 사이에 자식 컴포넌트를 넣는 방식이 아닌 `element`속성을 통해 자식 컴포넌트를 할당함

```
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";

const Router = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />}>
          <Route index element={<Home />} />
          <Route path="teams" element={<Teams />}>
            <Route path=":teamId" element={<Team />} />
            <Route path="new" element={<NewTeamForm />} />
            <Route index element={<LeagueStandings />} />
          </Route>
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

## Navigation

- `Link`컴포넌트를 통해 유저의 URL을 바꿀 수 있음

```
<Link to="/">Home</Link>
<Link to="about">About</Link>
```

## Reading URL Parameters

- v6 이상부터는 자동으로 `type|undefind`임을 알 수 있음(interface 필요없음)

```
import { useParams } from "react-router-dom";
...
<Routes>
  <Route
    path="items/:itemId"
    element={<Item />}
  />
</Routes>
...
const params = useParams();
return <h1>{params.itemId}</h1>
```

## useLocation()

```
// parent
<Link
  to={`/${coin.id}`}
  state={{ name: coin.name }}
>

//child
import { useLocation } from "react-router-dom";

interface RouteState {
  state: {
    name: string;
  };
}

const { state } = useLocation() as RouteState;
// v6부터는 제네릭을 지원하지 않음
```

## Nested Routes

- `Route`는 서로 중첩될 수 있음(부모를 상속하는 자식)
- 렌더링 위치는 부모 요소의`<Outlet />`의 위치를 따름

```
<Routes>
  <Route path="items" element={<Items />}>
    <Route path=":itemId" element={<Item />} />
    <Route path="sent" element={<SentItems />} />
  </Route>
</Routes>

...

function Items() {
  return (
    <div>
      <h1>Items</h1>
      <Outlet />
    </div>
  );
}
```

- URL에 따라 변경되는 내부 섹션이 있는 레이아웃에서 UI를 만드는데 적합함, 즉 한개의 루트 레이아웃에서 URL에 따라 일부 내부 컨텐츠만 변경되는 UI를 만들 수 있음

```
<Routes>
  <Route path="/" element={<Layout />}>
    <Route path="items" element={<Items />} />
    <Route path="another" element={<Another />} />
  </Route>
</Routes>

...

function Layout() {
  return (
    <div>
      <h1>Welcome to the app!</h1>
      <nav>
        <Link to="items">Items</Link> |{" "}
        <Link to="another">Another Items</Link>
      </nav>
      <div className="content">
        <Outlet />
      </div>
    </div>
  );
}
```
