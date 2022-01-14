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
const catchNoop = ([...arr]) => 
    (arr.forEach(a => a instanceof Promise ? a. catch(noop) : a), arr);

C.reduce = curry((f, acc, iter) => { iter ?
    reduce(f, acc, catchNoop(iter)) :
    reduce(f, catchNoop(acc));
});

C.take = curry((l, iter) => take(l, catchNoop(iter))));

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

## async/await
- 비동기적으로 일어나는 일들을 동기적인 문장으로 다룰 수 있게 해주는 키워드
- 어떤 함수를 await하기 위해서는 함수가 Promise를 리턴해야함
- async 함수를 선언하면 어떤 값을 return하던 Promise를 리턴함
```
function delay(a) {
    return new Promise(resolve => setTimeout(() => reselve(a), 500));
}

async function f1() {
    const a = await delay(10);
    const b = await delay(5);

    log(a + b);
}

// f1();
// f1().then(log);
// go(f1(), log);

// 아래와 같이도 사용가능
const pa = Promise.resolve(10);

(async () => {
    log(await pa);
});
```

## Array.prototype.map이 있는데 왜 FxJS의 map 함수가 필요한지?
- Array.prototype.map함수 자체가 비동기를 잘 제어 할 수 없음(async/await를 잘 사용할 수 없음)
- Promise가 들어있는 array를 주기 때문에 풀어줄 수 없음


## 비동기는 async/await로 제어할 수 있는데 왜 파이프라인이 필요한지?
- async/await : 원래 표현식으로 갇혀있는(ex.then.then...), 특정 부분에서 **함수 체인(합성)이 아니라 문장형(명령형)**으로 다루기 위한 목적(함수를 풀어놓으려는)
- 파이프라인(이터러블중심) : 명령형 프로그래밍을 하지 않고 더 안전하게 **함수 합성**을 하기위한 목적(동기/비동기 상황과는 연관X)

## async/await와 파이프라인을 같이 사용하기도 하는지?
```
async function f5(list) {
    const r1 = await go(list,
        L.map(a => delayI(a * a)),
        L.filter(a => delayI(a % 2)),
        L.map(a => delayI(a + 1)),
        C.take(2),
        reduce((a, b) => delayI(a + b)));

    const r2 = await go(list,
        L.map(a => delayI(a * a)),
        L.filter(a => delayI(a % 2)),
        reduce((a, b) => delayI(a + b)));

    const r3 = await delay(r1 + r2);

    return r3 + 10;
}
go(f5([1, 2, 3, 4, 5, 6, 7, 8]), a => log(a));
```

