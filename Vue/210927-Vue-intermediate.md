[인프런 Vue.js 중급 강좌 - 웹앱 제작으로 배워보는 Vue.js, ES6, Vuex](https://inf.run/fTnL) / [장기효(캡틴판교)](https://joshua1988.github.io/)  


# animation과 transition
- Vue에서는 애니메이션과 트랜지션을 코어 라이브러리 단에서 제공
- [Transitions & Animation - Vuejs 공식 가이드](https://vuejs.org/v2/guide/transitions.html)  


# slot
> 특정 컴포넌트의 일부 ui를 재사용할 수 있는 기능
- Modal로 예를 들면 dafault Modal을 만들어 놓고 Modal을 호출할때 상황에 맞는 내용을 slot부분에 넣을 수 있음(경고, 확인, 안내 등)
- template 내용을 들고오고 나서 다시 한번 재정의 할 수 있는 부분


# shorthand 축약형
- [v-on, v-bind Shorthand](https://vuejs.org/v2/guide/syntax.html#v-on-Shorthand)  


# transition-group
```
<transition-group name="list" tag="ul">
    <li>
        ...
    </li>
</transition-group>
```
- name은 css class와 관계
- tag는 transition effect가 들어갈 tag


# ES6(===ECMAScript 2015)
- 자바스크립트의 최신 문법
- 최신 FE Framework인 React, Anguler, Vue에서 권고하는 언어 형식
- ES5에 비해 문법이 간결
- 구 버전 브라우저 중 지원하지 않는 브라우저가 있으므로 transpiling 필요
- [ES6 docs - Babel](https://babeljs.io/docs/en/learn.html)  
- Babel -> JavaScript compiler


# const & let
> 새로운 변수 선언 방식
- 기존의 변수 선언 방식은 유연하면서 애매모호함
- 블록 단위 `{}`로 변수의 범위가 제한됨
- `const` : 한번 선언한 값을 변경할 수 없음(상수 개념) / 객체나 배열의 내부는 변경 가능
- `let` : 한번 선언한 값을 다시 선언할 수 없음


# ES5의 특징
### 변수의 Scope
- ES5는 `{}`에 상관없이 스코프가 설정됨

### Hoisting
- 선언한 함수와 변수를 해석기가 가장 상단에 있는 것처럼 인식함
- 코드의 라인 순서와 관계없이 함수선언식(function statement)과 변수를 위한 메모리 공간을 먼저 확보 *함수표현식(function expression)은 해당 안됨*
- 함수선언과 변수선언 먼저, 대입 및 할당은 나중에

### Arrow Function
- [ES6 Arrow function](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)  
- 화살표 함수
- `function` 키워드 대신 `=>`로 대체
- 콜백 함수의 문법을 간결화
```
var sum = function(a, b) {
    return a + b;
};

var sum = (a, b) => {
    return a + b;
};

var arr = ["a", "b", "c"];
arr.forEach(function(value) {
    console.log(value);
});

arr.forEach(value => console.log(value));
```

### Enhanced Object Literals
- 향상된 객체 리터럴
- 객체의 속성을 메소드로 사용할 때 `function` 예약어를 생략하고 생성 가능
```
var dict = {
    lookup: function() {
        ...
    }
};

var dict1 = {
    lookup() {
        ...
    }
};
```

### 속성명 축약
```
components:{
    //왼쪽과 오른쪽이 같으면 축약 가능
    //위아래 같음
    'ComponentA' : ComponentA,
    ComponentA
}
```

### Modules
- 모듈 로더 라이브러리(AMD, Commons JS) 기능을 js언어 자체에서 지원
- 호출되기 전까지는 코드 실행과 동작을 하지 않는 특징
- export & import
- `default export` : 한개의 파일에서 하나만 export, 가져다 쓸 때 이름을 부여해서 사용



# Vuex 상태 관리 라이브러리
- 복잡한 app의 컴포넌트들을 관리하는 상태 관리 패턴이자 라이브러리
- React의 Flux 패턴에서 기인함
- 단방향 데이터 흐름

### Flux
- MVC 패턴의 복잡한 데이터 흐름 문제를 해결하는 개발 패턴 - Unidirectional data flow
- Flux 패턴 : Action -> Dispatcher -> Model(Store) -> View (단방향)
- MCV 패턴 : Controller -> Model <-> View (양방향)

### Vuex가 필요한 이유
- 데이터를 전달하기 위해 거쳐야할 컴포넌트가 많을 때
- 컴포넌트 간 데이터(이벤트) 전달이 명시적이지 않음
- 여러 개의 컴포넌트에서 같은 데이터를 업데이트 할 대 동기화 문제

### Vuex 구조
- 컴포넌트 -> 비동기 로직 -> 동기 로직 -> 상태
- Vue Components -> Actions -> Mutations -> State

### Vuex 설치하기
- [vuex - 공식 문서](https://vuex.vuejs.org/kr/)  
```
npm i vuex --save

package.json 에서 확인

// 관행적으로 사용하는 폴더
src/store/store.js
```
- Vuex 등록하기
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex);

export const store = new Vuex.Store({
    // store.js
});

// main.js에서 vue에 store를 등록
```


# Vuex 기술 요소
- **state** : 컴포넌트 간에 공유하는 데이터 `data`
- state가 변경되면 vue reactivity에 의해 화면 갱신

```
state: {
    message: 'Hello'
}

<p>{{ this.$store.state.message }}</p>
```

- **getters** : 연산된 state 값을 접근하는 속성 `computed`
```
state: {
    num: 10
},
getters: {
    getNumber(state) {
        return state.num;
    }
}

<p>{{ this.$store.getters.getNumber }}</p>
```

- **mutations** : 유일하게 state 값을 변경하는 이벤트 로직, 메서드 `methods`
- state를 변경할 때 mutations을 이용하는 이유 : 어떤 컴포넌트에서 해당 state를 변경했는지 명확하게 추적하기 위해
```
state: { num: 10 },
mutations: {
    sumNums(state, anotherNum) {
        return state.num + anotherNum;
    }
}

this.$store.commit('sumNums', 20);
// mutations를 동작시킬 때 인자(payload)를 전달할 수 있음
// 인자는 한개만 전달 할 수 있으므로 두개 이상을 전달 할때는 {} 객체로
```

- **actions** : 비동기 처리 로직을 선언하는 메서드 `async methods`
- 비동기 로직을 담당하는 mutations(ex.데이터 요청, Promise, ES6 async)
```
// store.js
mutations: {
    addCnt(state) {
        state.cnt++;
    }
},
actions: {
    delayAddCnt(context) {
        setTimeout(() => context.commit('addCnt');, 2000);
    }
}
// App.vue
methods: {
    incrementCnt() {
        this.$store.dispatch('delayAddCnt');
    }
}
```

***Q. 왜 비동기처리 로직은 꼭 actions에 선언해야 하는가?***  
***A. 시간차를 두고 여러 컴포넌트에서 state를 변경하는 경우, state 값의 변화를 추적하기 어렵기 때문에***  


# Helper 함수
> Store에 있는 속성들을 간편하게 코딩하는 방법
- Helper 함수들은 인자를 명시하지 않아도 호출 단에서 인자를 넘겨줬다면 그대로 들고감
***너무 신기하다...***  
```
import { mapState, mapGetters, mapMutations, mapActions } from 'vuex'

```
- **...** : ES6의 Object Spread Operator, 객체 속성들을 모두 가져옴
```
let kim = {
    name: 'yoon',
    lang: 'js'
};
let company = {
    team: 'A',
    // name: kim.name,
    // lang: kim.lang
    ...kim
};
// 기존의 컴포넌트에 존재하는 computed속성과 mapGetters를 함께 사용하기 위해 사용함
```

## mapState
- Vuex에 선언한 state 속성을 뷰 컴포넌트에 더 쉽게 연결 해줌
```
computed() {
    ...mapState(['num'])
    // num() { return this.$store.state.num; }
}
state: {
    num:10
}

<p>{{ this.num }}</p>
<!-- <p>{{ this.$store.state.num }}</p> -->
```

## mapGetters
- Vuex에 선언한 getters 속성을 뷰 컴포넌트에 더 쉽게 연결 해줌
```
computed() {
    // 연결할 getters와 이름이 다르면 []배열이 아니라 객체로{ 현재컴포넌트에서의 이름 : '실제 getters이름' }
    ...mapGetters(['reverseMessage'])
}

getters: {
    reverseMessage(state) {
        return state. ,,,
    }
}
...
<!-- <p>{{ this.$store.getters.reverseMessage }}</p> -->
<p>{{ this.reverseMessage }}</p>
```


***Q. computed는 왜 사용하는가?***
***A. 템플릿에서 사용하는 복잡한 로직은 computed에서 사용. 재사용성 증가. mapState와 mapGetters를 computed에서 사용하는 이유.***  


## mapMutations, mapActions
- Vuex에 선언한 mutations, actions 속성을 뷰 컴포넌트에 더 쉽게 연결 해줌
```
methods: {
    ...mapNutations(['clickBtn']),
}

mutations: {
    clickBtn(state) {
        alert(state.str);
    }
}

<button @click="clickBtn">str</button>
```


## 프로젝트 구조화와 모듈화
- **store속성의 모듈화**
    - state, getters, mutations, actions 각각의 파일로
```
// store.js
import * as mutations from './mutations'

export const store = new Vuex.Store({
    state: {
        ,,,
    },
    mutations
});

// mutations.js
const clearItems = (state) => {
    ,,,
}

export { clearAllItems }

// or
export const clearItems = (state) => {
    ,,,
}

```


- **store의 모듈화**
    - 앱의 규모가 커서 1개의 store로 관리가 힘들때 `modules`속성 사용
```
// store.js
import todo from 'modules/todo.js'

export const store = new Vuex.Store({
    modules: {
        moduleA: todo, //or
        todo
    }
});

// todo.js
const state = {},,,
```