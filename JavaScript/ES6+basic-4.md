[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

## 결과를 만드는 함수 reduce, take
- 실제로 연산을 시작하는 시작점을 알리는 함수

## reduce
```
L.entries = fuction *(obj) {
    for (const k in obj) yield [k, obj[k]];
};

// Array.prototype.join보다 다형성이 높은 join함수
const join = curry((sep = ',', iter) =>
    reduce((a, b) => '${a}${sep}${b}', iter));

// const queryStr = obj => go(
//   obj,
const queryStr = pipe(
    L.entries,
    L.map(([k, v])=> '${k}=${v}'),
    join('&');

//    Object.entries,
//    map(([k, v])=> '${k}=${v}'),
//    reduce((a, b) => '${a}&${b}')
);

log(queryStr({ limit: 10, offset:10, type:'notice'}));
```

## take, find
- find는 take를 통해 결론(결과)을 지어서 만들 수 있음
```
const users = [
    { age: 32 },
    { age: 43 },
    { age: 34 },
    { age: 25 },
    { age: 21 },
    { age: 38 },
    { age: 23 },
];

// 첫번째로 만나는 1개만 꺼내주는 함수
const find = curry((f, iter) => go(
    iter,
    L.filter(f)
    take(1)
    ([a]) => a
));

log(find(u => u.age < 30, users ));
```

## L.map + take로 map 만들기
```
const takeAll = take(Infinity);

L.map = curry(function *(f, iter) {
    for (const a of iter) {
        yield f(a);
    }
});

const map = curry(pipe(L.map, takeAll));

log(map(a => a + 10, L.range(4)));
```

## L.filter + take로 filter 만들기
```
L.filter = curry(fuction *(f, iter) {
    for (const a of iter ) {
        if (f(a)) yield a;
    }
});

const filter = curry(pipe(L.filter, takeAll));

log(filter(a => a % 2, range(4)));

```

## L.flatten
```
// 바로 평가되는 flatten 함수
const flatten = pipe(L.flatten, takeAll);

const isIterable = a => a && a[Symbol.iterator];

// 깊은 Iterable을 모두 펼칠 때
L.deepFlat = function*(iter) {
    for (const a of iter) {
        if (isIterable(a)) yield *f(a);
        else yield a;
    }
}

L.flatten = function *(iter) {
    for (const a of iter) {
        if (isIterable(a)) yield *a;
//        if (isIterable(a)) for (const b of a) yield b;
// yield *iterabel = for (const val of iterable) yield val;
        else yield a;
    }

var it = L.flatten([[1,2], 3, 4, [5, 6], [7, 8, 9]]);
log([...it]);
};
```
- 1차원 배열로 만들어주는 제너레이터를 반환하는 함수


## L.flatMap
```
// 두 방법은 큰 차이가 없음(똑같이 전부 순회하기 때문)
// 기존의 flatmap은 array에서만 동작함
log([1, 2], [3, 4], [5, 6, 7].flatMap(a => a.map(a => a * a)));
log(flatten([1, 2], [3, 4], [5, 6, 7].map(a => a.map(a => a * a))));

L.flatMap = curry(pipe(L.map, L.flatten));

//즉시평가
const flatMap = curry(pipe(L.map, flatten));

var if = L.flatMap(map(a => a * a), [[1, 2], [3, 4], [5, 6, 7]]);
log([...it]);

```

## 2차원 배열 다루기
```
const arr = [
    [1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [9, 10]
];

go(arr,
    L.flatten,
    L.filter(a => a % 2),
    L.map(a => a * a),
    take(3),   
    reduce(add),
    log);
```

## 지연성 / 이터러블 중심 프로그래밍 실무적인 코드 예제
```
var users = [
    { name: 'a', age: 21, family: [
        { name: 'a1', age: 56 }, { name: 'a2', age: 70 },
        { name: 'a3', age: 15 }, { name: 'a4', age: 3 }
    ]},
    { name: 'b', age: 38, family: [
        { name: 'b1', age: 34 }, { name: 'b2', age: 5 }
    ]},
    { name: 'c', age: 31, family: [
        { name: 'c1', age: 68 }, { name: 'c2', age: 62 },
        { name: 'c3', age: 12 }
    ]},
    { name: 'd', age: 20, family: [
        { name: 'd1', age: 42 }, { name: 'd2', age: 42 },
        { name: 'd3', age: 11 }, { name: 'd4', age: 4 }
    ]},
]

go(users,
    L.map(u => u.family),
    L.flatten,
    L.filter(u => u.age < 20),
    L.map(u => u.name),
    take(4),
    log);

```
