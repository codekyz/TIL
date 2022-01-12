[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

# callback과 Promise
- callback : 인자와 callback함수를 받아서 정의함
```
function add10(a, callback) {
    setTimeout(() => callback(a + 10), 100);
}

add10(5, res => {
    // 연속실행
    add10(res, res => {
        log(res);
    })
})
```

- Promise : Promise를 만들어서 return해줌
```
function add20(a) {
    return new Promise(resolve => setTimeout(() => resolve(a+20), 100));
}

add20(5)
    // 연속실행
    .then(add20)
    .then(log);
```

## callback과 Promise의 차이
- Promise는 일급 값으로 비동기 상황을 다룸(일급 = 인자, 변수, 리턴값 등으로 사용될 수 있음)
- Promise라는 클래스를 통해 만들어진 인스턴스를 반환하는데, 대기,성공,실패를 다루는 일급값으로 이루어져 있음
- Promise는 코드를 평가했을때 즉시 Promise객체가 반환됨
- Promise는 객체를 이용해 이후에 일들을 연결지어서 해나갈 수 있음
- callback은 비동기 상황을 코드와 컨텍스트로만 다룸(실행하고 나면 아무것도 이어나갈 수 없음)


## 값으로서 Promise 활용
```
const deley100 = a => new Promise(resolve => 
    setTimeout(() => resolve(a), 100));

const go1 = (a, f) => a instanceof Promise ? .then(f) : f(a);
const add5 = a => a + 5;

const n1 = 10;
log(go1(go1(n1, add5), log));

const n2 = deley100(10);
log(go1(go1(n2, add5), log));
```


## 함수합성 관점에서의 Promise와 모나드
- 함수합성 : `f.g == f(g(f))`
- 모나드 : 함수 합성을 할때 안전하게 합성할 수 있게 하기 위한 도구(중요X)
- Promise : 비동기 상황을 안전하게 합성하는 것


## Kleisli Composition 관점에서의 Promise
- `f.g` `f(g(x)) = f(g(x))` 오류가 났을 때는 이 합성이 성립되지 않음
- Kleisli Composition : 특정한 규칙을 만들어서 합성을 안전하게 만들고 수학적으로 바라볼 수 있게 만들어 주는 것
- `f(g(x)) = g(x)` : g에서 에러가 난 경우에는 같은 결과가 성립될 수 있음(Kleisli Composition)
- (같은 Promise객체를 반환하므로 위와 같은 결과가 성립됨)
- `Promise.reject` : 에러가 날 경우 reject된 Promise를 리턴함


## go, pipe, reduce에서 비동기 제어
- ex) test/es6_code.html - 39 line


## Promise.then의 중요한 규칙
- 아무리 여러번의 Promise가 중첩되어도 안쪽에 있는 '값'을 한번의 then으로 꺼낼 수 있음
```
Promise.resolve(Promise.resolve(Promise.resolve(1))).then(log);
// 1

new Promise(resolve => resolve(new Promise(resolve => resolve(1))))).then(log);
// 1
```

