# Next-NodeBird

- [[리뉴얼] React로 NodeBird SNS 만들기](https://inf.run/4WeP)

## React, Next를 사용하는 주된 목적

- 고객의 경험(모바일 앱을 사용하는 것과 같은 경험)
- 서버 사이드 랜더링(검색엔진)

## 코드스플릿팅

- CSR 에서 접속한 페이지에 대한 부분, 코드만 쪼개서 가지고 옴

## eslint

- 코드룰(컨벤션)을 정해줌

```
npm i eslint -D
npm i eslint-plugin-import -D
npm i eslint-plugin-react -D
npm i eslint-plugin-reac-hooks -D
```

```
// .eslintrc

{
  "parserOptions": {
    "ecmaVersion": 2022,
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "extends": ["eslint:recommended", "plugin:react/recommended"],
  "plugins": ["import", "react-hooks"],
  "rules": {}
}
```

## \_app.js와 AppLayout.js

- \_app.js는 pages의 공통 부분
- Layout은 일부 컴포넌트끼리의 공통 부분
