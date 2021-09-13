[캡틴판교님의 포스팅을 읽고 정리했습니다](https://joshua1988.github.io/web-development/javascript/js-async-await/)

# JavaScript의 비동기 처리
> 비동기 처리란? 어떤 코드의 연산의 결과를 기다리지않고 다음 코드를 먼저 실행하는 특성


#### Example
1. jQuery ajax
2. setTimeout() - Web API의 한 종류로 지정한 시간만큼 기다렸다가 실행
- 문제점 -> **코드 작성은 1-2-3 이어도 실제 실행은 1-3-2**


## Callback함수로 문제점 해결
> 콜백함수를 사용하면 **특정 로직이 끝났을 때에만** 원하는 동작을 실행


#### Callback hell 콜백 지옥
> 콜백 함수를 연속해서 사용할 때 발생하는 문제
- 해결방법 -> 코딩 패턴으로 개선 or Promise, Async 사용


## Promise
> 자바스크립트 비동기 처리에 사용되는 객체로 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용

[Promise - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)


#### Promise의 세가지 상태
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태 `new Promise()`
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태 `resolve(), then()`
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태 `reject()` 실패한 이유를 `catch()`로 받을 수 있음


#### Promise Chaining
- `then()` 메서드를 호출하고 나면 새로운 프로미스 객체가 반환되고 이를 이용해 여러 개의 프로미스를 연결하여 사용할 수 있음


#### Promise Error Handling(reject()가 호출된 실패 상태)
1. `then()`의 두 번째 인자로 에러를 처리
2. `catch()` 이용하기
- 1번의 경우 `then()`의 첫 번째 콜백 함수 내부에서의 오류를 제대로 잡아내지 못함 따라서 더 많은 예외 처리 상황을 위해 가급적 2번`catch()`사용


## async & await
> 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 패턴으로 기존의 비동기 처리 방식인 callback과 promise의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 함

- async & await example
```
async function logName() {
    var user = await fetchUser('domain.com/users/1');
    if (user.id === 1) {
        console.log(user.name);
    }
}
```

- callback func example
```
function logName() {
    var user = fetchUser('domain.com/users/1', function(user) {
        if (user.id === 1) {
            console.log(user.name);
        }
    });
}
```


#### async & await 기본 문법
```
async function 함수명() {
    await 비동기_처리_메서드_명();
}
```
1. 함수 앞에 `async`라는 예약어를 붙임
2. 함수의 내부 로직 중 HTTP통신을 하는 비동기 처리 코드 앞에 `await`를 붙임
    * 비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 `await`가 의도한대로 동작함
3. `await`의 대상이 되는 비동기 처리 코드는 axios 등 프로미스를 반환하는 API 호출 함수


#### async & await 장점
- callback이나 promise보다 짧은 코드와 가독성
- 기존의 비동기 처리 코드 방식으로 사고하지 않아도 됨


#### async & await 예외 처리
> `try catch` 문법 사용

