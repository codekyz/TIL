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
- ex) test/es6_code.html - 39 line go1()


## Promise.then의 중요한 규칙
- 아무리 여러번의 Promise가 중첩되어도 안쪽에 있는 '값'을 한번의 then으로 꺼낼 수 있음
```
Promise.resolve(Promise.resolve(Promise.resolve(1))).then(log);
// 1

new Promise(resolve => resolve(new Promise(resolve => resolve(1))))).then(log);
// 1
```

## 지연 평가 + Promise - L.map, map, take
- 지연평가와 비동기 동시성을 지원하는 함수
```
const go1 = (a, f) => a instanceof Promise ? a.then(f) : f(a);

const take = curry((l, iter) => {
    let res = [];
    // 재귀
    return function recur() {
        for (const a of iter) {
            if (a instanceof Promise) return a
                .then(a =>  (res.push(a), res).length == l ? res : recur())
                // Kleisli Composition 활용
                .catch(e => e == nop ? recur() : Promise.recject(e));
            res.push(a);
            if (res.length == l) return res;
        }
        return res;
    } ();
});

L.map = curry(function *(f, iter) {
    for(const a of iter) {
        yield go1(a, f);
});

go(
    // [1, 2, 3]
    [Promise.resolve(1), Promise.resolve(2), Promise.resolve(3)],

    // L.map(a => a + 10),
    // L.map(a => Promise.resolve(a + 10)),

    // map은 L.map, takeAll을 하는 함수
    map(a => Promise.resolve(a + 10)),
    // takeAll,
    log);
```

## Kleisli Composition - L.filter, filter, nop, take
- 필터에서 지연평가와 비동기 동시성, Promise를 지원하려면 Kleisli Composition을 활용해야함
- `Promise.reject()`를 하게되면 모든 `.then`을 무시하고 `.catch`로 감
```
// 아무일도 하지않는다는 구분자
const nop = Sybol('nop');

L.filter = curry(function *(f, iter) {
    for(const a of iter) {
        const b = go1(a, b);
        if (b isinstanceof Promise) yield b
            .then(b => b ? a : Promise.reject(nop));
        else if (f(b)) yield a;
    }
});

go([1, 2, 3, 4, 5, 6],
    L.map(a => Promise.resolve(a * a)),
    L.filter(a => a % 2),
    L.map(a => a * a),
    take(4),
    log);
```

## reduce에서 nop지원
- 지연평가와 비동기 동시성을 지원하는 reduce
```
const reduceF = (acc, a, f) => 
    a instanceof Promise ? 
        a.then(a => f(acc, a), e => e == nop ? acc : Promise.recject(e)) : 
        f(acc, a);

const head = iter => go1(take(1, iter), ([h]) => h);

const reduce = curry((f, acc, iter) => {
    if (!iter) return reduce(f, head(iter = acc[Symbol.iterator](), iter);

    iter = iter([Symbol.iterator]());
    return go1(acc, function recur(acc) {
        let cur;
        while(!(cur = iter.next()).done) {
            acc = reduceF(acc, cur.value, f);
            if (acc instanceof Promise) return acc.then(recur);
        }
    });
    return acc;
});

go([1, 2, 3, 4],
    L.map(a => Promise.resolve(a * a)),
    L.filter(a => Promise.resolve(a % 2)),
    reduce(add),
    log);
```

## 지연 평가 + Promise의 효율성
- 모든 값을 평가하고 그 중에서 `take`하는게 아니라 원하는 값을 `take`하고 나면 나머지는 아예 평가하지 않음
