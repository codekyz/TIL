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
