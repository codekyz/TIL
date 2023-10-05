[udemy 클린코드 자바스크립트](https://www.udemy.com/course/clean-code-js/)

## 몽키패치 = 안티패턴

- 런타임 중인 프로그램의 내용이 변경되는 행동을 의미

# 변수 다루기

- var를 지양하자
- var는 함수 스코프 < let과 const는 블록 스코프
- let보다는 const(재할당의 차이)

  - 객체, 배열 조작에는 영향을 주지 않음

- 전역공간(최상위) 사용 최소화(global-node.js환경, window-브라우저환경)

  - 즉시실행함수, module, 클로저, const, let 사용
  - 전역변수X 지역변수O window, global 조작X
  - **스코프를 나누는 방법에 대해 고민**

- 임시변수 제거하기

  - 함수를 잘게 쪼개기(하나의 역할만 하는 함수)
  - **함수내에서 임시변수를 조작하는 것은 좋지 않음**
  - 바로 반환(return)
  - 고차함수(map, filter, reduce)사용
  - 선언형으로 작성

- 호이스팅(선언과 할당의 분리) 주의하기
  - 함수도 호이스팅됨
  - const로 함수 표현식 작성하는 것을 추천

# 타입 다루기

- 동적 타이핑 언어로 타입검사가 어려움
- `typeof` : 타입을 문자열로 반환
  - 원시값은 판별해내지만 참조값은 그렇지 않음
  - null은 'object'로 나오는 언어적 오류
- `kim instanceof Person` : 객체의 프로토타입 체인을 검사
  - 최상위에 있는 Object와도 같음
- `Object.ptorotype.toString.call(arr)` : 최상위에 있는 Object를 활용

- `undefined` : 선언했지만 값은 정의되지 않고 할당X, 연산에는 NaN으로 취급
- `null` : 무언가 없음을 명시적으로 표현하는 방법, 연산에는 0으로 취급

  - 둘 중 어떤 값을 사용할지 컨벤션으로 정의를 하자

- eqeq 줄이기

  - 동등연산자(==)는 형변환이 일어남
  - 엄격한 동등연산자(===) 사용하기

- 형변환 주의하기

  - 암묵적인 형변환(+, !!)
  - 명시적인 형변환(String, Boolean, Number, parseInt)
  - -> 예측하기 쉬운 코드작성

- isNaN 사용 주의하기
  - `isNaN` : 느슨한 검사
  - `Number.isNaN` : 엄격한 검사

# 경계 다루기

- min / max

  - **해당 값을 포함을 하는지 안하는지 포함 여부가 중요**
  - 이상, 초과 vs 이하, 미만
  - 혹은 네이밍에 포함여부를 작성한다

- begin / end

  - begin은 포함
  - end는 포함되지 않음
  - ex 숙박 날짜 예약

- first / last

  - 포함된 양 끝을 의미
  - first 부터 last 까지

- prefix / suffix

  - ex) react use~~~(Hooks)
  - ex) js getter setter, #
  - ex) component naming

- 매개변수의 순서가 경계다
  - 호출하는 함수의 네이밍과 인자의 순서의 연관성을 고려한다
  - 매개변수는 2개가 넘지 않도록 만들기
  - arguments, rest parameter 사용하기
  - 매개변수를 객체에 담아서 넘기기
  - 랩핑하는 함수 만들기

# 분기 다루기

- 값식문

  - `()` 함수의 실행과 관련
  - JSX에서 `{}` 안에는 값과 식만 들어가야함
  - 삼항연산자 -> 값으로 귀결될 수 있는 식

- 삼항연산자 다루기

  - 삼항연산자 사용에 대한 일관성 중요
  - 조건 ? 참(식) : 거짓(식)
  - 조건이나 식이 헷갈리는 경우 괄호로 감싸기
  - void한 함수를 삼항연산자에 사용할 경우 undefined

- Truthy and Falsy

  - Truthy === 참 같은 값
  - Falsy === 거짓 같은 값(undefined, null)
  - [mdn](https://developer.mozilla.org/ko/docs/Glossary/Truthy)

- 단축평가 short-circuit evaluation

  - `||`, `&&`

- else if 피하기

  - else if문은 else처리를 한번 하고 if문을 사용하는거와 같음
  - else if가 늘어지면 switch 고려하기

- else 피하기
- Early Return

  - 함수를 미리 종료
  - 최상위에 거르는 로직을 위치시킴
  - 사고하기 편함

- 부정조건문 지양하기

  - 생각을 여러번 해야할 수 있음
  - Early Return, Form Validation, 보안 혹은 검사하는 로직에는 사용하게 될 수 있음

- Default Case 고려하기

  - edge case 고려하기
  - 사용자 실수 예방하기

- 명시적인 연산자 사용 지향하기

  - 괄호사용
  - 예측가능하고 디버깅하기 쉬운 코드

- Nullish coalescing operator

  - `??` null 병합 연산자, null과 undefined에 대해 평가할때만 사용

- 드모르간의 법칙

# 배열 다루기

- JavaScript의 배열은 객체다

  - key와 value로 값을 넣을 수 있음
  - `Array.isArray(arr)` : 배열확인 빌트인 메서드

- Array.length 주의하기

  - `Array.length` : 배열에 길이보다 마지막 인덱스에 가까움
  - ex) 임의의 숫자를 할당하면 해당 배열의 인덱스가 늘어남
  - ex) 0을 할당하면 초기화 됨
  - **length를 조작해도 Array에 영향이 감**

- 배열 요소(element)에 접근하기

  - `[first, second ...] = inputs` : 구조분해 할당
  - arr[0], arr[1]... 이런 방식의 접근 줄이기

- 유사 배열 객체

  - ex) arguments, 매개변수를 선언하지 않아도 유사배열 객체로 들어오게됨
  - 유사 배열 객체는 map과 같은 고차함수를 사용할 수 없음

- 불변성(immutable) 지키기

  - 1. 배열을 복사한다
  - 2. 새로운 배열을 반환하는 메서드들을 활용한다
    - filter, map, slice...

- for문, 배열 고차 함수로 리팩토링
- 배열 메서드 체이닝 활용하기

  - ex) arr.filter().sort().map() ...

- map vs forEach

  - `return의 차이`
    - forEach는 반환 값이 undefined로 **요소마다 콜백함수를 실행**하기만 함
    - map은 콜백함수의 반환 값이 저장되어 **새로운 배열을 반환** 함
  - 실행만 시키는 경우에는 forEach를 사용

- Continue & Break
  - 특정 레이블이나 문의 흐름을 제어함
  - **forEach나 map, filter 등에서 사용 불가능(문법오류)**
  - for문을 쓰거나 try...catch문을 사용
  - 혹은 every, some, find, findIndex와 같은 배열 메서드와 조합하여 사용

# 객체 다루기

- Shorthand Properties(축약 문법)를 잘 알고 일관성있게 사용하자

  - Concise Method(간결한 메소드)
  - ES2015+, 모던 자바스크립트 문법

- Computed Property Name

  - 동적으로 들어오는 값도 프로퍼티 네임으로 활용할 수 있음
  - ex) `setState({[e.target.name]: e.target.value});`
  - ES2015+, 모던 자바스크립트 문법

- Object Lookup Table(순람표)

  - key와 value로 나열된 데이터 구조
  - if나 switch문이 늘어질 경우

  ```
  function getUserType(type) {
    const USER_TYPE = {
      ADMIN: "관리자",
      INSTRUCTOR: "강사",
      STUDENT: "수강생",
    };
    return USER_TYPE[type] || "해당 없음";
  }

  // 바로 리턴하는 형태
  function getUserType(type) {
    return (
      {
        ADMIN: "관리자",
        INSTRUCTOR: "강사",
        STUDENT: "수강생",
      }[type] ?? "해당 없음"
    );
  }
  ```

  - 상수를 따로 관리하는 형태가 베스트
  - 불필요한 분기문을 줄이는 예

- Object Destructuring(객체 구조 분해 할당)

  - `(name, { age, location })` : name은 필수, 나머지는 옵션
  - `const { 0: first, 2: third } = orders vs const [first, , third] = orders`

- Object.freeze(객체 동결)

  - `Object.isFrozen(obj)` : 동결이 잘 되었는지 확인하는 메서드
  - shallow copy vs deep copy
    - deep freezing이 되지않음(depth가 있는 경우)
    - 중첩된 freezing이 필요함
  - deepFreeze 유틸함수
    - 1. 객체를 순회
    - 2. 값이 객체인지 확인
    - 3. 객체이면 재귀
    - 4. 그렇지 않으면 return Object.freeze(obj)
  - TypeScript => readonly 키워드 사용

- Prototype 조작 지양하기

  - 이미 JS는 많이 발전(직접 만들어서 모듈화하기 => 배포)
  - 빌트인 객체를 건들지 말자
  - prototype을 건드는 것은 몽키패칭 언어이기 때문에 위험

- hasOwnProperty(프로퍼티를 가졌느냐)

  - 보호를 받지 못하기 때문에 아래와 같이 call해서 사용
  - `Object.prototype.hasOwnProperty.call(foo, "bar");`

- 직접 접근 지양하기
  - 직접 접근해서 값을 변경X, 함수에 위임하여 추상화O
  - 데이터에 접근할 때는 항상 안전하게 접근
