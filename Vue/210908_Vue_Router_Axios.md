[인프런 Vue.js 시작하기 - Age of Vue](https://inf.run/C898/) / [장기효(캡틴판교)](https://joshua1988.github.io/vue-camp/)

# 같은 컴포넌트 레벨 간의 통신
> 위에서 아래로는 props, 아래서 위로는 event
- 규칙에 맞게 상위 컴포넌트로 event를 올려주고 다시 props로 내려줘서 통신함

# Vue Router
```
var router = new VueRouter({
    // url의 해쉬 값 제거 속성
    mode: 'history',
    // 페이지의 라우팅 정보 속성
    routes: [
        // 로그인 페이지 정보
        {
            // 페이지의 url
            path: '/login',
            // 해당 url에서 표시될 컴포넌트
            component: LoginComponent
        },
        // 메인 페이지 정보
        {
            path: '/main',
            component: MainComponent
        }
    ]
});
```
- router-view : 라우터가 표시되는 영역
- router-link : 라우터에서 페이지 이동을 위한 링크(=/ `<a>`)
`<router-link to="/login"></router-link>`

#### Navigation guard*
> 뷰 라우터로 특정 url에 접근할 때 인증 정보가 없으면 접근하지 못하게 할 때 사용하는 기술

[캡틴판교님 블로그 글](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/, "네비게이션 가드")

# vscode 단축키
- 같은 텍스트 선택 : Ctrl + d
- 사이드바 토글 : Ctrl + b 

# Axios
> 뷰에서 권고하는 Promise(자바스크립트의 비동기 처리 패턴)기반의 HTTP 통신 라이브러리

[Vue Resource](https://github.com/pagekit/vue-resource)
과거의 공식 라이브러리

[Ajax - wikipedia](https://ko.wikipedia.org/wiki/Ajax)

[jsonplaceholder - 샘플데이터 제공](https://jsonplaceholder.typicode.com/)