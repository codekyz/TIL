[인프런 Vue.js 시작하기 - Age of Vue](https://inf.run/C898/) / [장기효(캡틴판교)](https://joshua1988.github.io/vue-camp/)


# Watch 속성
> data에 변화가 있을 때 특정 로직을 실행하는 속성

```
watch: {
    //newValue:갱신된 값, oldValue:이전 값
    //data 변화를 계속 추적하기 때문에 이전 값과 갱신된 값 모두 받을 수 있음
    data: function(newValue, oldValue) {
        실행 할 로직;
    }
}
```


## Watch vs Computed
>되도록이면 computed를 쓰는게 좋고 watch보다는 computed가 대부분의 케이스에 적합. computed로 할 수 있는 일을 watch로 할 필요 없음


[Computed와 Watch 비교 공식문서](https://v3.vuejs.org/guide/computed.html#computed-vs-watched-property)


#### Computed
- 뷰 내부적으로 계산을 하는 속성
- 데이터 의존성
- 빠른 계산, 단순 계산
- validation, 간단한 텍스트 연산
```
computed: {
    errorTextColor: function() {
        //삼항 연산자
        return this.isError ? 'warning' : null;
    }
}
```

#### Watch
- 무거운 로직, 매번 실행되기 부담되는 로직
- 데이터 요청
- method를 엮어서

