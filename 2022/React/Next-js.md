# Next.js

- React Framework

## Static Pre Redering

- next.js에 의해 초기상태로 HTML이 미리 렌더링됨

## pages

- file name = url route name
- index = home page
- component name은 중요하지 않음
- 404 page를 제공
- `homepage/movies` = `pages/movies/index.js` 폴더 구조에 따라 맵핑
- 페이지가 하나라면 폴더를 만들 필요 없음

## routing

[routing공식문서](https://nextjs.org/docs/routing/introduction)
[router공식문서](https://nextjs.org/docs/api-reference/next/router)

- Link component 존재
- Link is only for 'href'
- className, style ... a tag에 작성

```
<nav>
  <Link href="/">
    <a>Home</a>
  </Link>
  <Link href="/about">
    <a>About</a>
  </Link>
</nav>

or

const router = useRouter();
const onClick = (id: number) => {
  router.push(`/movies/${id}`);
};

or

const router = useRouter();
const onClick = (id: number, title: string) => {
  router.push(
    {
      pathname: `/movies/${id}`,
      query: {
        title,
      },
    },
    `/movies/${id}`
  );
};
```

## Dynamic routes

[공식문서](https://nextjs.org/docs/routing/dynamic-routes)

- `homepage/movies/:id` = `pages/movies/[id].js`

## Styled-jsx

[공식문서](https://nextjs.org/docs/basic-features/built-in-css-support#css-in-js)

- 해당 컴포넌트 스코프 내로 적용범위가 한정됨

```
<style jsx>{`
  nav {
    background-color: tomato;
  }
  a {
    text-decoration: none;
  }
`}</style>

// global로 적용(하위컴포넌트까지 적용)
// but, 페이지가 다르면 적용안됨
<style jsx global>{`
  nav {
    background-color: tomato;
  }
  a {
    text-decoration: none;
  }
`}</style>
```

## CSS Modules

- random class name을 만들어줌

```
// 1
import styles from "./NavBar.module.css";

const NavBar = () => {
  const router = useRouter();
  return (
    <nav className={styles.nav}>
...

// 여러 클래스네임을 적용할 때
// 2
<Link href="/">
  <a
    className={`${styles.link} ${
      router.pathname === "/" ? styles.active : ""
    }`}
  >
    Home
  </a>
</Link>

// 3
<Link href="/">
  <a
    className={[
      styles.link,
      router.pathname === "/" ? styles.active : "",
    ].join(" ")}
  >
    Home
  </a>
</Link>
```

## Custom App

[공식문서](https://nextjs.org/docs/basic-features/typescript#custom-app)

- 여기서 GlobalStyles를 추가해줄수 있음
- custom app에서만 css import가 가능(다른 페이지나 컴포넌트에서는 module이어야함)

```
// Component => 렌더링하길 원하는 페이지
import type { AppProps } from 'next/app'

const App = ({ Component, pageProps }: AppProps) => {
  return (
    <>
      <NavBar />
      <Component {...pageProps} />
    </>
  );
};
```

## Layout

[공식문서](https://nextjs.org/docs/basic-features/layouts)

- \_app 파일이 무거워지지 않도록 Layout을 활용

```
// components/Layout
import NavBar from "./NavBar";

type LayoutProps = {
  children: React.ReactNode;
};

export default function Layout({ children }: LayoutProps) {
  return (
    <>
      <NavBar />
      <div>{children}</div>
    </>
  );
}

// _app
const App = ({ Component, pageProps }: AppProps) => {
  return (
    <Layout>
      <Component {...pageProps} />
    </Layout>
  );
};

```

## Redirects

[공식문서](https://nextjs.org/docs/api-reference/next.config.js/redirects)

## Rewrite

[공식문서](https://nextjs.org/docs/api-reference/next.config.js/rewrites)

## Server Side Rendering

[공식문서](https://nextjs.org/docs/api-reference/data-fetching/get-server-side-props#getserversideprops-with-typescript)

- `getServerSideProps()` : 서버측에서만 실행되는 코드
