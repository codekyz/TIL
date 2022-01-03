[인프런 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://inf.run/fTnL) / [장기효(캡틴판교)](https://joshua1988.github.io/)


# 스타일 가이드
- 스크립트 내 컴포넌트 : 파스칼 케이스
- 템플릿 내 컴포넌트 : 케밥 케이스


# 기본 설정(index.html)
#### viewport
[viewport](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag)  
`<meta name="viewport" content="width=device-width, initial-scale=1">`
- 반응형 태그

#### favicon
- [favicon generator](https://www.favicon-generator.org/)  

#### Awesome font
- [Awesome font](https://fontawesome.com/account/cdn)  

#### Google font
- [Google font](https://fonts.google.com/specimen/Ubuntu#standard-styles)  


# css scoped
- 컴포넌트 내에서만 style이 유효하도록


# localStorage
- [localStorage - MDN](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)  
`localStorage.setItem(key, value);`
- 크롬 개발자 도구 -> application탭에서 확인
- setItem, remove, clear


# Vue Life Cycle*
1. created : 생성되는 시점


# v-for
```
<li v-for="todoItem in todoItems" v-bind:key="todoItem">
    ...
</li>

//인덱스 사용(index는 0부터)
<li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow">
    ...
    <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
        ...
    </span>
</li>
```


# splice()
```
this.todoItems.splice(index, 1);
```
- 자바스크립트 api
- [Array.protorype.splice() - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)  


***Q. 왜 지우는건 바로 적용되고 새로 추가되는건 바로 안되지?***
***A. remove는 list내에서 실행하고 add는 input에서 실행함. 서로 통신을 하고 있지 않은 상태임.  input에서 새로운 아이템을 추가하면 스토리지내에는 저장되지만 list컴포넌트로는 전달이 안되므로 나타나지 않음. remove는 list내의 data인 todoitems에서 수행됨***


# JSON.stringify
```
JSON.stringify(obj);
```
- 자바스크립트 객체를 string으로 변환해주는 api
- 변환하지 않고 넘기면 object안에 뭐가 들었는지 확인이 안됨


# JSON.parse
```
console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));

```
- JSON.stringify로 가져온 값은 String이기 때문에 다시 객체로 변환 해줌

**localStorage 특성상 JSON 필요**
- localStorage에서는 update불가능. 변경이 있을때 remove하고 다시 set함


# v-bind:class
```
<span v-bind:class="{textCompleted: todoItem.completed}">
...
</span>
```
- 값에 따라 클래스가 달라짐


# Container와 Presenter
- Container component : 동작, 데이터 조작(비지니스 로직)에 관련된 컴포넌트
- Presenter component : 단순하게 화면을 표현하는 컴포넌트


***Q. list에 item을 추가할 때 마지막으로 추가된건 아래로 가는데, 다시 갱신했을 때는 왜 순서가 바뀔까?***
***A. 로컬 스토리지에서 아이템을 가져올 때 localStorage.key()라는 API를 사용하는데 이 API는 브라우저마다 각기 다른 방법으로 키를 접근하기 때문. 일관적인 순서를 유지하려면 sort() 이용.***


# 안티 패턴 anti-pattern*
- 많이 사용되는 패턴이지만 비효율적이거나 비생산적인 패턴
- 현재 강의에서는 컨테이너에서 내려준 데이터를 프레젠터가 다시 컨테이너로 올려주고 그 데이터를 조작하는 것이 해당


# 관심사 분리 SoC(separation of concerns)
- 각 컴포넌트들이 서로 다른 관심사를 갖도록 프로그램을 여러 부분으로 분리하는 설계(디자인) 원칙


