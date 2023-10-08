[udemy React 완벽 가이드](https://www.udemy.com/share/105mrW3@Q3RxcNbt1xBgyR0JHG3qMbtlkBVXSv8zPt4uOrKTxUugM1xrd1U0qZ-LmUNRjOjQSQ==/)

# JavaScript Refresher

## 웹사이트에 JavaScript 추가하기

1. `<script>` tags
2. `<script src=''>` import/export
   1. `type = "module"` 로 설정되어 있어야 함
   2. 코드를 쪼개서 관리하기 위함

### React의 빌드 프로세스(가 필요한 이유)

- React는 `JSX` 문법을 사용하는데 이는 브라우저에서 실행이 불가능함
- 따라서 브라우저에 전달하기 전에 코드가 수정될 필요가 있음
- 더 자세히 설명하면 `react-scripts` 라이브러리가 브라우저에 전달될 HTML파일에 `<script>` 태그를 추가해서 간소화되고 최적화된 JS파일을 import함
- `CRA`, `Vite`를 사용하면 빌드 프로세스가 탑재되어 있어 별도의 설정이 필요없음

## JavaScript Basic

### 변수와 상수

- 변수 : `let`
  - `var`의 문제점 : 블록 스코프가 없으며(함수 수준의 스코프) 중복 선언을 허용함 또한 함수가 시작되는 시점(스크립트가 시작되는 시점)에 처리됨
- 상수 : `const` 재할당X, 의도가 명확, 읽기전용

### 함수

- `function` 키워드
- `() =>` 화살표 함수
  - 익명함수를 정의할 때
  - 매개변수가 1개일 때만 ()생략가능
  - 반환문(return)만 있는 경우 return과 {}생략가능

### 객체와 클래스

- 내부에서 메소드(함수) 생성 가능
- 본인의 프로퍼티에 접근 시 `this` 키워드 사용
- `constructor()` 생성자 함수

### 배열

- `[value1, value2, ...]`
- 특별한 유형의 객체이자 값 type
- `array.[method name]` : 내장 유틸리티 메소드
  - ex) `findIndex` `map`(새 배열을 반환)

### Destructuring

- 배열과 객체의 분해

```
//array
const [firstName, lastName] = ["Yoonjung", "Kim"]

//object
const {name: userName, age} = {
  name: "Yoonjung",
  age: 29
};
```

- 함수 매개변수 목록의 분해

```
//하나의 매개변수(객체)만 받는 것
function storeOrder({id, currency}) {
  ...
}
```

### Spread Operator

- `...`

```
//array
const mergedArray = [...array1, ...array2]

//object
const extendedObject = {
  newKey: true,
  ...oldObject
}
```

[Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
