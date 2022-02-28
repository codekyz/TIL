# TypeScript

[공식문서](https://www.typescriptlang.org/)

- JavaScript 기반의 프로그래밍 언어
- TypeScript is JavaScript with syntax for types
- 코드 실행 '전' 타입 실수나 오류를 막기위한 안전장치

```
const plus = (a:number, b:number) => a + b;
```

## Installation (w/React)

```
npx create-react-app my-app --template typescript
```

#### CRA, styled-components 오류 발생 시

```
// Type definition
npm i --seve-dev @types/styled-components
```

# TypeScript 개요

## 타입 추론 Types by Inference

- TS는 JS를 기반으로 하기 때문에 대부분의 경우 타입을 생성해줌
- 생성과 동시에 특정 값을 할당하는 경우, 그 값을 해당 변수의 타입으로 사용함

## 타입 정의 Defining Types

- 몇몇 디자인 패턴은 자동으로 타입을 제공하기 힘들 수 있음
- 따라서 명시가능한 JS의 확장을 지원함
  ```
  const user = {
    name: "Hayes",
    id: 0,
  };
  ```
  이 객체의 형태를 명시적으로 나타내기 위해서 `interface`로 선언함
  ```
  interface User {
    name: string;
    id: number;
  };
  ```
  변수 선언 뒤에 `: TypeName`의 구문을 사용해 객체가 `interface`의 형태를 따르고 있음을 선언할 수 있음
  ```
  const user: User = {
    name: "Hayes",
    id: 0,
  };
  ```
  `interface`는 클래스로도 선언할 수 있음
  ```
  class UserAccount {
    name: string;
    id: number;
    constructor(name: string, id: number) {
      this.name = name;
      this.id = id;
    }
  }
  const user: User = new UserAccount("Murphy", 1);
  ```
  `interface`는 함수에서 매개변수와 리턴 값을 명시하는데 사용되기도 함
  ```
  function getAdminUser(): User {
    //...
  }
  function deleteUser(user: User) {
    // ...
  }
  ```

## 타입 구성 Composing Types

- 여러 타입을 이용하여 새 타입을 작성하기 위한 방법으로 `유니언Union`과 `제네릭Generic`이 있음

### 유니언 Unions

- 타입이 여러 타입중 하나일 수 있음을 선언하는 방법
- 유니언이 가장 많이 사용되는 사례 중 하나는 다음과 같이 허용되는 string 또는 number의 리터럴 집합을 설명하는 것

```
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

- 함수가 다양한 타입을 처리하는 방법을 제공함

```
function getLength(obj: string | string[]) {
  return obj.length;
}
```

### 제네릭 Generics

- 제네릭은 타입에 변수를 제공하는 방법
- 제네릭이 있는 배열은 배열 안의 값을 설명할 수 있음

```
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;
```

## 구조적 타입 시스템 Structural Type System

- TS의 핵심 원칙 중 하나는 타입 검사가 값이 있는 **형태**에 집중한다는 것
- 때때로 `duck typing` 또는 `structural typing`이라고 불림
- 구조적 타입 시스템에서 두 객체가 같은 형태를 가지면 같은 것으로 간주됨

```
interface Point {
  x: number;
  y: number;
}

function printPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}

// "12, 26"를 출력합니다
const point = { x: 12, y: 26 };
printPoint(point);
```

- 객체 또는 클래스에 필요한 모든 속성이 존재한다면, TS는 구현 세부정보에 관계없이 같은 것으로 봄
