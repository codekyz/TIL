[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

# 병렬적 로직
- 많은 자원을 사용해서 빠른처리

## C.reduce, C.take
- 지연된 함수열을 병렬적으로 평가하기
```
const C = {};

// 아무일도 하지않는 함수
function noop() {}

// catch 에러 방지
const catchNoop = arr => 
    (arr.forEach(a => a instanceof Promise ? a. catch(noop) : a), arr);

C.reduce = curry((f, acc, iter) => { 
    // catch 에러 방지
    const iter2 = catchNoop(iter ? [...iter] : [...acc]);
    return iter ? 
        reduce(f, acc, iter2) :
        reduce(f, iter2));
}

C.take = curry((l, iter) => take(l, catchNoop([...iter]))));

const delay1000 = a => new Promise(resolve =>
    setTimeout(() => resolve(a), 1000));

go([1, 2, 3, 4, 5],
    L.map(a => delay1000(a * a)),
    L.filter(a => delay1000(a % 2)),
    C.take(2),
    C.reduce(add),
    log);

```
- `Promise.reject` 후에 `.catch`를 하게 되면 정확하게 에러 처리는 되지만 이미 찍힌 에러 로그는 어떻게 할 수 없음
- 따라서 미리 `.catch`를 해주면 됨

## 즉시 병렬적으로 평가하기 C.map, C.filter
- 
```
C.takeAll = C.take(Infinity);

C.map = curry(pipe(L.map, C.takeAll));
C.filter = curry(pipe(L.filter, C.takeAll));

C.map(a => delay1000(a * a), [1, 2, 3, 4]).then(log);
C.filter(a => delay1000(a % 2), [1, 2, 3, 4]).then(log);
```

## 즉시, 지연, Promise, 병렬적 조합하기
