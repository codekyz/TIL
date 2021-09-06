인프런 Vue.js 시작하기 - Age of Vue / 장기효(캡틴판교) https://inf.run/C898
https://joshua1988.github.io/vue-camp/
MVVM 패턴 https://black-jin0427.tistory.com/133
IIFE https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty
Reactivity https://v3.ko.vuejs.org/guide/reactivity.html#%E1%84%87%E1%85%A1%E1%86%AB%E1%84%8B%E1%85%B3%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC-reactivity-%E1%84%8B%E1%85%B5%E1%84%85%E1%85%A1%E1%86%AB
this https://www.w3schools.com/js/js_this.asp

# Vue란?
> MVVM 패턴의 뷰모델(ViewModel) 레이어에 해당하는 화면(View)단 라이브러리
- DOM Listeners
- Data Bindings

#### MVVM 패턴*
> Model - View - ViewModel Pattern
> 1. View(UI)
> 2. Model(UI상에 보여지고 있는 데이터)
> 3. Glue code(핸들링과 바인딩 그리고 비즈니스 로직)

# 즉시실행함수 IIFE
> 즉시 실행되어 값으로 의미를 가지는 함수

# Vue의 reactivity(반응성)
> 반응성이란? '변경'에 대한 제어를 선언적으로 수행하는 프로그래밍 패러다임
- vue는 비간섭적인 반응성 시스템
- vue에서 모델은 프록시로 감싸진 자바스크립트 객체로 모델을 변경하면, 화면이 바뀜

# Vue Instance
```new Vue();```
함수 앞글자가 대문자 -> 생성자 함수
#### 뷰 인스턴스의 속성과 api
> 생성자의 인자는 객체로 key-value
- el:
- template: 화면에 표시될 html,css
- data: reactivity가 반영된 데이터
- methods:
- created:
- watch:

#### vue를 생성자 함수로 찍어내는 이유
vue에서 api와 속성들을 정의해놓고 가져다 쓰는 방식으로 재사용성을 높힘

# Components
- 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능, 재사용성 up
- 모던 프레임워크는 대부분 컴포넌트를 기반으로 함
- 인스턴스를 생성하면 기본적으로 root 컴포넌트가 됨

#### 지역 컴포넌트와 전역 컴포넌트의 차이
##### 지역 컴포넌트
- 일반적인 등록 방식, 하단에 어떤게 등록되어 있는지 알 수 있음
- 인스턴스를 생성할때마다 다시 등록해줘야함

##### 전역 컴포넌트
- 플러그인이나 라이브러리 형태로 전역으로 사용해야하는 컴포넌트만 등록
- 인스턴스를 생성할때마다 다시 등록할 필요없음

# 컴포넌트 통신 규칙
> 컴포넌트는 각각 고유한 데이터 유효 범위를 가짐
> 상위에서 하위로 데이터를 내려줌 -> **props**
> 하위에서 상위로 이벤트를 올려줌 -> **이벤트 발생**

#### 컴포넌트 통신 규칙이 필요한 이유
n방향 통신에서는 문제가 발생했을 때 추적하기 어려움
컴포넌트 통신 규칙에서는 데이터가 위에서 아래로만 내려가고
아래에서 위로는 이벤트만 올려줌
데이터와 이벤트가 뒤죽박죽으로 돌지 않음

# this
- this를 쓰면 해당 객체를 보게 됨
- data에 있는 값들은 객체가 가지고 있는 것과 같음

