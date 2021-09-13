[인프런 Vue.js 시작하기 - Age of Vue](https://inf.run/C898/) / [장기효(캡틴판교)](https://joshua1988.github.io/vue-camp/)


# Axios 호출 전 후의 this 차이
- Axios 호출 전의 `this` : 인스턴스나 컴포넌트를 바라보는 this (뷰모델)
- Axios 호출 후의 `this` : 비동기 처리를 하면서 실행 컨텍스트가 바뀌면서 this의 내용도 바뀜
- (콘솔에서 직접 확인해보니 호출 전의 this는 Vue, 호출 후의 this는 window라고 뜬다)


# 클라이언트(브라우저)와 서버의 HTTP 통신 구조
1. HTTP Request(요청) : 브라우저(클라이언트) -> 서버
2. 백엔드 로직 : 서버
3. 데이터 요청 : 서버 -> DB
4. 데이터 응답 : DB -> 서버
5. 백엔드 로직 : 서버
6. HTTP Response(응답) : 서버 -> 브라우저(클라이언트)


#### 크롬 개발자 도구 Network
- Headers : HTTP 정보
- Preview : Response의 내용을 구조화해서 볼 수 있음


[크롬 개발자도구 공식문서](https://developer.chrome.com/docs/devtools/)



# Template
> 템플릿 문법이란 뷰로 화면을 조작하는 방법

- 데이터 바인딩
- 디렉티브


## 데이터 바인딩
> 뷰 인스턴스에서 정의한 속성들을 화면에 표시하는 방법 (콧수염 괄호 Mustache Tag)

```
<div>{{ message }}</div>
```
```
new Vue({
    data: {
        message: 'Hello Vue.js'
    }
})
```


## 디렉티브
> 뷰로 화면의 요소를 더 쉽게 조작하기 위한 문법 (v-...)

```
<div>
    <span v-if="show">
        Hello
    </span>
    <span v-else>
        Vue.js
    </span>
    <span v-show="show">
        Hi
    </span>
</div>
```
```
new Vue({
    data: {
        show: false
    }
})
```

#### v-if와 v-show의 차이점
- v-if 사용 시에는 DOM에서 해당 엘리먼트가 아예 제거됨
- v-show 사용 시에는 DOM에는 남아있고 `style="display: none;"`이 적용됨


#### 키보드 입력 이벤트
```
//enter를 입력할 때만 logText를 실행
<input type="text" v-on:keyup.enter="logText">
```



[Vuejs 공식 가이드](https://vuejs.org/v2/api/#v-on)


