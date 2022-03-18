## gh-pages

```
npm i gh-pages

// package.json 가장 상단
"homepage" : "Githubpages URL"
.
.
.
"deploy" : "gh-pages -d build"
"predeploy": "npm run build"
```

- 빌드 후 빌드한 파일이 github pages로 올라가게됨
- predeploy를 추가로 작성하면 deploy실행 시 먼저 predeploy를 실행하고 deploy가 실행됨

### React project

```
<BrowserRouter basename={process.env.PUBLIC_URL}>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="movie/:id" element={<Detail />} />
  </Routes>
</BrowserRouter>
```

- App.js에서 basename을 설정해줘야 경로오류가 안남
