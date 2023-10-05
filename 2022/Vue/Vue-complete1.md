[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://inf.run/QXkN) / [장기효(캡틴판교)](https://joshua1988.github.io/)  

## esLint란?
- 문법 검사 도구
- 사용자 스타일에 따라 코딩 규칙을 추가할 수 있음
- *ex 트레일링 콤마 trailing comma, ;*
```
//vue.config.js
module.exports = {
    lintOnSave: false
    //lint 끄기
}
```

## Router
[Vue Router 정리](https://github.com/codekyz/TIL/blob/main/Vue/Vue2_Router_Axios.md)  
- 버전업되면서 조금 달라졌을 수 있음
- [vue-news](https://github.com/codekyz/vue-news) 프로젝트 참고

### router-link
- 자동으로 a태그로 변환해줌
- `<router-link to="/news">News</router-link>`

## API
- `src/api/index.js` : API 함수들을 정리

## Lifecycle hooks
[Vue.js 공식문서 - Lifecycle Hooks](https://v3.vuejs.org/guide/composition-api-lifecycle-hooks.html)


## this
1. 전역에서 this === `window`
2. 함수 안에서의 this === `window`
3. 생성자 함수 안에서 this === `객체 instance`
4. 비동기 처리에서의 this === 호출 후 `undefind`
    - 화살표 함수를 사용하면 호출 전의 this를 가지고 옴


## Callback, Promise
[자바스크립트 비동기 처리 - Callback과 Promise](https://github.com/codekyz/TIL/blob/main/JavaScript/Asynchronous_processing.md)
- Callback 함수의 문제점 : Callback이 중첩되었을 때 절차적 사고에 위배되는 결과가 나옴(콜백지옥)
- Promise 등장 : 효율적인 Callback관리와 직관적 코드 목적

## Dynamic Route Matching 동적 라우트 매칭
[Vue.js 공식문서 - Dynamic Route Matching](https://router.vuejs.org/kr/guide/essentials/dynamic-matching.html)
```
{
    path: '/user/:id',
    component: UserView,
},
```