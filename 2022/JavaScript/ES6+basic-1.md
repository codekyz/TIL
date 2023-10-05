[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

### 함수형 프로그래밍

##### 일급 함수
- 자바스크립트에서 함수는 값으로 다룰 수 있음(인자, 변수, 리턴값 등)
- 조합성과 추상화의 도구

##### 고차 함수
- 함수를 값으로 다루는 함수(함수를 인자로 받아서 실행하는 함수)
- 함수를 만들어 리턴하는 함수(클로저를 만들어 리턴하는 함수)


## ES6의 리스트 순회
> 기존의 for문과 달라짐
```
for (const a of list){
    log(a);
}
```
**내장 이터러블**
- `Array`
- `Set` `Map` : 기존 for문으로 순회 불가
- `map.keys()`키만 뽑아줌 `map.values()`값만 뽑아줌 `map.entries()`키와 값


## 이터러블/이터레이터 프로토콜
> 이터러블을 for..of, 전개 연산자 등과 함께 동작하도록한 규약

- 이터러블 : 이터레이터를 리턴하는 `[Symbol.iterator]()` 를 가진 값
- 이터레이터 : `{ value, done }` 객체를 리턴하는 `next()` 를 가진 값 (순회를 하다가 done이 true가 되면 빠져나옴)

## 사용자 정의 이터러블
```
const iterable = {
    [Symbol.iterator]() {
        let i = 3;
        return {
            next() {
                return i == 0 ? { done: true } : { value: i--, done: false }
            },
            // 이터러블을 이터레이터로 만든 후에 실행해도 순회가 되어야 함
            [Symbol.iterator]() { return this; }
        }
    }
};
let iterator = iterable[Symbol.iterator]();
for (const a of iterable) log(a);

//이터레이터가 자기 자신 또한 이터러블이면서 자기 자신을을 반환할 때 잘 구현된 이터러블이라고 할 수 있음
```
- 내장 되지 않은 외부 라이브러리의 이터러블도 심볼 이터레이터가 구현되어 있으면(이터러블/이터레이터 프로토콜을 따른다면) 순회할 수 있음

## 전개 연산자
> 이터러블/이터레이터 프로토콜을 따르는 객체들을 전개할 수 있음
- `...` 전개 연산자


## 제너레이터
> 이터레이터이자 이터러블을 생성(리턴)하는 함수
```
// 일반 함수에서 *을 붙여서 만듬
function *gen() {
    yield 1;
    if (false) yield 2;
    yield 3;
    return 100;
    //리턴값도 반환할 수 있음(done이 true가 될때)
}

for (const a of gen()) log(a);

//odds 예제
function *ifinity(i = 0) {
    while (true) yield i++;
}
function *limit(l, iter) {
    for (const a of iter) {
        yield a;
        if (a == l) return;
    }
}
function *odds(l) {
    for(const a of limit(l, ifinity(1))) {
        if (a % 2) yield a;
    }
}
```
- 문장을 이용해 순회할 값을 작성하는 제너레이터를 이용해 어떠한 값이든 순회하도록 만들 수 있음

## 구조 분해, 나머지 연산자
```
log(...odds(10));
log([...odds(10), ...odds(20)]);

const [head, ...tail] = odds(5);
log(head);
log(tail);

const [a, b, ...rest] = odds(10);
log(a);
log(b);
log(rest);

```

*220107 그냥 그렇구나 하고 넘어갔던 제너레이터의 동작에 대해 어느정도 이해할 수 있었다. 여러번 반복해서 보고 연습해봐야겠다*