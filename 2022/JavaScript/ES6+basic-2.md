[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

## map 함수
```
const map = (f, iter) => {
    let res = [];
    for (const p of iter) {
        res.push(f(p));
        // 어떤 값을 넣을지 보조 함수에 위임
    }
    return res;
}

log(map(p => p.name, products));
```
- 내장 map함수는 array의 프로토타입에 작성
- 위와 같이 이터러블 프로토콜을 따른 map 함수는 모든 것들을 map할 수 있음
```
let m = new Map();
m.set('a', 10);
m.set('b', 20);
log(new Map(map(([k, v]) => [k, v * 2], m)));
```

## filter
```
const filter = (f, iter) => {
    let res = [];
    for (const a of iter) {
        if (f(a)) res.push(a);
        // 어떤 조건을 줄지 보조 함수에 위임
    }
    return push;
};
```
-- 위와 같이 이터러블 프로토콜을 따른 filter 함수는 모든 것들을 filter할 수 있음

## reduce
```
const reduce = (f, acc, iter) => {
    if (!iter) {
        iter = acc[Symbol.iterator]();
        acc = iter.next().value;
    }
    for (const a of iter) {
        acc = f(acc, a);
    }
    return acc;
};
```
- 특정한 값을 순회하면서 누적해 나갈때 사용

#### 중첩 사용
- `map` `filter` `reduce` 중첩 사용이 가능
```
log(
    reduce(
        add,
        map(p => p.price,
            filter(p => p.price < 20000, products))));
    )
)
```

## 코드를 값으로 다루어 표현력 높이기
#### go
```
const go = (...args) => reduce((a, f) => f(a), args);

go(
    0,
    a => a + 1,
    a => a + 10,
    a => a + 100,
    log
);
// 111

go(
    products,
    products => filter(p => p.price < 20000, products,
    products => map(p => p.price, products),
    prices => reduce(add, prices),
    log);
)
// 위 중첩된 코드를 읽기 쉽도록 개선

go(
    products,
    filter(p => p.price < 20000),
    map(p => p.price),
    reduce(add),
    log);
)
// curry를 통해 보다 간결하게 개선(filter, map, reduce에 curry적용)
```

#### pipe
```
const pipe = (...fs) => (a) => go(a, ...fs);

const f = pipe(
    a => a + 1,
    a => a + 10,
    a => a + 100,
);
log(f(0));
// 111
```

#### curry
```
const curry = f =>
    (a, ..._) => _.length ? f(a, ..._) : (..._) => f(a, ..._);
// 함수를 받아서 함수를 리턴하는데 함수가 실행되었을 때
// 인자가 두개 이상이라면 받아둔 함수를 즉시실행하고
// 한개라면 함수를 다시 리턴한 후에 이후에 받은 인자를 합쳐서 실행하는 함수

const mult = curry((a, b) => a*b);
log(mult(1)(3));
// 3

const mult3 = mult(3);
log(mult3(10));
log(mult3(5));
log(mult3(3));
// 30 15 9
```

## 함수 조합으로 함수 만들기
```
const total_price = pipe(
    map(p => p.price),
    reduce(add));

const base_total_price = predi => pipe(
    filter(predi),
    total_price);

go(
    products,
    base_total_price(p => p.price < 20000),
    log);
)

```