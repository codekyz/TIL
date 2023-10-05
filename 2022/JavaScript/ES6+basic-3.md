[인프런 함수형 프로그래밍과 JavaScript ES6+](https://inf.run/3PMF) / [유인동](https://www.inflearn.com/users/31989)  

## range
```
const range = l => {
    let i = -1;
    let res = [];
    while (++i < l) {
        res.push(i);
    }
    return res;
};

// range값 모두 더하기
var list = range(4);
log(list);
log(reduce(add, list));

```
- range를 실행한 즉시 배열로 평가가 됨(값이 만들어짐)


## 느긋한 L.range
```
const L = {}
L.range = function *(l) {
    let i = -1;
    while (++i < l) {
        yield i;
    }
};

// range값 모두 더하기
var list = L.range(4);
log(list); // 이터레이터
log(reduce(add, list));

```
- 이터레이터의 내부를 실제로 순회할 때 마다 값이 하나씩 평가가 됨(함수내부에서는 평가X, next할때 평가됨)
- 배열을 만들지 않고 하나씩 값을 꺼내기만 함
- 조금 더 효율적이라고 볼 수 있음(지연성)

## take
```
const take = (l, iter) => {
    let res = [];
    for (const a of iter) {
        res.push(a);
        if (res.length == l) return res;
    }
    return res;
}
// 많은 값을 받아서 잘라주는 함수
log(take(5, range(10000)));
// 비효율적
log(take(5, L.range(10000)));
// 효율적
```
- 지연성은 연산을 하지 않고 있다가 take나 reduce같은 함수를 만날 때 연산을 처음하는 기법


## 이터러블(리스트) 중심 프로그래밍에서의 지연 평가 Lazy Evaluation
- 제때 계산법(영리한 계산법)
- 느긋한 계산법
- 제너레이터/이터레이터 프로토콜을 기반으로 구현


## L.map
```
L.map = function *(f, iter) {
    for(const a of iter) yield f(a);
};
// next를 통해 평가하는 값만 얻어올 수 있음
// L.map 자체는 배열을 만들지 않음
```
- 평가를 미루는 성질을 가지고 평가순서를 달리 조작할 수 있는 준비가 되어있는 이터레이터를 반환하는 제너레이터 함수


## L.filter
```
L.filter = function *(f, iter) {
    for(const a of iter) if (f(a)) yield a;
};
```
- 마찬가지로 함수를 수행하는 동안에는 평가가 이루어지지 않음


### range, map, filter, take, reduce 중첩 사용
```
go(range(10),
    map(n => n + 10),
    filter(n => n % 2),
    take(2),
    log);
```
- 위부터 순서대로 평가하면서 내려옴


### L.range, L.map, L.filter, take, reduce 중첩 사용
```
go(L.range(10),
    L.map(n => n + 10),
    L.filter(n => n % 2),
    take(2),
    log);
```
- 아래서 위로 다시 위에서 아래로 세로로 평가됨
- 최종적으로 take할 수만큼만 동작하기 때문에 range의 수가 아무리 많아도 시간은 똑같음


### map, filter 계열의 함수들이 가지는 결합 법칙
- 사용하는 데이터가 무엇이든지
- 사용하는 보조 함수가 순수 함수라면 무엇이든지
- 아래와 같이 결합한다면 둘 다 결과가 같음
- ex) [[mapping, mapping], [filtering, filtering], [mapping, mapping]] == [[mapping, filtering, mapping], [mapping, filtering, mapping]]


### ES6의 기본 규약을 통해 구현하는 지연 평가의 장점
-  서로 다른 라이브러리, 다른 사람이 만든 함수여도 기본 규약을 기반으로 함으로 안전한 방식으로 합성할 수 있음