[udemy JavaScript 알고리즘 & 자료구조 마스터클래스](https://www.udemy.com/course/best-javascript-data-structures/)

# big O Notation 빅오 표기법

- 입력의 크기와 실행시간의 관계
- 가장 높은 실행 시간을 의미
- 빅오 표기법에서 상수는 중요하지 않음

속도(시간 복잡도)
메모리사용(공간 복잡도)
읽기 쉬운 코드

## 1. 시간 복잡도(속도)

```
function addUpToFirst(n) {
  let total = 0;
  for (let i=1; i<=n; i++) {
    total += i;
  }
  return total;
}
// O(n)

function addUpToSecond(n) {
  return n * (n+1) / 2;
}
// O(1)

console.log(addUpToFirst(6));
console.log(addUpToSecond(6));

// 1.실행 시간의 비교

let t1 = performance.now();
// 브라우저가 이 문서를 만든 시간, 이 창이 열린 시간을 알려줌
addUpToFirst(100000000);
let t2 = performance.now();
console.log(`Time Elapsed: ${(t2-t1) / 1000} seconds.`);
// 완전히 신뢰할 수 없는 방식
// 기계마다 사양에 따라 다름
// 같은 기계여도 다른 타임이 기록 됨
// 너무 빠른 알고리즘의 속도 차이를 측정하기 힘듬

// 2. 컴퓨터가 처리해야하는 연산(operation) 갯수 카운팅
// - 정확한 연산 갯수는 중요치 않음, 전체적인 추세가 중요
// - Performence Tracker

function countUpAndDown(n) {
console.log("Going up!");
for (let i = 0; i < n; i++) {
console.log(i);
}
// O(n)
console.log("At the top!\nGoing down...");
for (let j = n; j >= 0; j--) {
console.log(j);
}
// O(n)
console.log("Back down. Bye!");
}
// O(n)

function printAllPairs(n) {
for (var i = 0; i<n; i++) {
for (var J = 0; j < n; j++) {
console.log(i,j);
}
// O(n)
}
// O(n)
}
// O(n\*n) 중첩되어 있으면 제곱
```

## 2. 공간 복잡도(메모리)

```
// - 보조 공간 복잡도 : 입력을 제외한 알고리즘 자체가 필요로 하는 공간을 의미
// - bool, num, undefined, null = 불변 공간
// - 문자 = O(n) 공간을 필요
// - reference types, array, object = O(n)

function sum(arr) {
let total = 0;
for (let i = 0; i = arr.length; i++) {
total += arr[i];
}
return total;
}
// O(1) space

function double(arr) {
let newArr = [];
for (let i = 0; i < arr.length; i++) {
newArr.push(2 \* arr[i]);
}
return newArr;
}
// O(n) space

+) log

이진로그 = 2의 몇승이?
빅오표기법에서의 log는 log2(이진로그)
```

## 배열과 오브젝트의 성능 평가

### Objects

- 객체는 정렬이 필요없을 때 사용
- 빠른 접근, 입력과 제거를 원할 때 좋음
- 정렬은 되어 있지 않지만 다른 것들은 매우 빠름

big O of Objects

- insertion = O(1)
- Removal = O(1)
- Searching = O(n)
- Access = O(1)

big O of Object Mehtods

- Object.keys = O(n)
- Object.values = O(n)
- Object.entries = O(n)
- hasOwnProperty = O(1)

### Arrays

- 정렬된 리스트, 정렬이 필요할 때 사용
- 인덱스가 있음

big O of Arrays

- Insertion = It depends / 어디에 입력하는지에 따라 다름
  맨 뒤에 push() = O(1), 맨 앞에 = O(n)
- Removal = It depends / 어디에 있는 것을 제거하는 지에 따라 다름
- Searching = O(n)
- Access = O(1) / 인덱스가 있기 때문

big O of Array Operations

- push = O(1)
- pop = O(1)
- shift = O(n)
- unshift = O(n)
- concat = O(n)
- slice = O(n)
- splice = O(n)
- sort = O(n\*log n)
- forEach/map/filter/reduce/etc. = O(n)

---

## Algorithm

문제 해결 접근법

1. 문제의 이해
   - 문제 자체에 대한 이해
2. 구체적 예시
   - 입/출력값, 에러, 입력오류, 예외 등
3. 세부 분석
   - 의사코드, 또는 주석
4. 해결 또는 단순화
   - 실제 코드 작성, 해결할 수 있는 부분부터 처리
5. 되돌아 보기와 리팩터 Refactor
   - 리팩토링

```
// 문제 해결 패턴
// 1. 빈도 카운터 Frequency Counters

function same(arr1, arr2) {
  if(arr1.length !== arr2.length){
    return false;
  }
  for(let i = 0; i < arr1.length; i++){
    let correctIndex = arr2.indexOf(arr1[i] ** 2)
    if(correctIndex === -1) {
      return false;
    }
    arr2.splice(correctIndex,1)
    // arr2에서 삭제
  }
  return true;
}

// O(n2)
// 두개의 중첩된 루프보다 그냥 두개의 루프가 훨씬 낫다

function same(arr1, arr2) {
  if(arr1.length !== arr2.length) {
    return false;
  }
  let frequencyCounter1 = {}
  let frequencyCounter2 = {}
  for(let val of arr1) {
    frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
  }
  for(let val of arr2) {
    frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1
  }
  for(let key in frequencyCounter1){
    if(!(key ** 2 in frequencyCounter2)) {
      return false;
    }
    if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
      return false;
    }
  }
  return true;
}

// O(n)

// Anagrams 도전 과제
// 두 개의 문자열을 취하여 두 문자열이 서로 아나그램이면 참이 반환
// 문자의 종류와 갯수(빈도)가 일치해야 함
// 공백, 특수문자, 숫자, 대소문자는 고려하지 않음

function vaildAnagram(first, second) {
  if (first.length !== second.length) {
    return false;
  }

  const lookup = {};

  for(let i = 0; i < first.length; i++) {
    let letter = first[i];
    // if letter exists, increment, otherwise set to
    lookup[letter] ? lookup[letter] += i : lookup[letter] = 1;
  }

  for(let i = 0; i < second.length; i++) {
    let letter = second[i];
    // can't find letter or letter is zero then it's not an anagram
    if(!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }

  return true;
}
```
