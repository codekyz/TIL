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
