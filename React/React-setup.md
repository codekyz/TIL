# 구성

- styled-components
- recoil
- react-router-dom
- react-hook-form
- react-query

## CRA Installation (w/TS)

```
npx create-react-app my-app --template typescript
```

## Packages

```
npm i styled-components

// Type definition
npm i --seve-dev @types/styled-components

npm i react-router-dom

npm i recoil

npm i react-hook-form

npm i react-query
```

# 폴더구조

- 간단한 어플리케이션을 만들 때는 폴더 구조가 그리 중요하지 않았으나 점차 복잡해지면서 구조를 정의할 필요성을 느낌
- 아직 큰 프로젝트를 경험해보지 못 했기 때문에 일단은 내 경험을 토대로 공통 컴포넌트들을 빼서 관리하는 것부터 시작해보기로 했음.

```
public/
    index.html

src/
    App.tsx
    index.tsx
    api/
        api.ts

    components/ -- 공통 컴포넌트 관리
        Button.tsx
        Input.tsx
            Home/ -- 특정 페이지에서만 사용되는 컴포넌트 관리
              ImgCard.tsx

    pages/ -- 컴포넌트로 구성된 페이지 관리
        LogIn.tsx
        Home.tsx

    routes/ -- router 관리
        router.ts

    recoil/ -- atoms 관리
        atom.ts

    styles/ -- style 관련 파일 관리
        GlobalStyle.ts
        styled.d.ts
        theme.ts
```
