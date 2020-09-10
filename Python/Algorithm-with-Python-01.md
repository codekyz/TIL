
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 1장 알고리즘 기초

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## 사전 or 사후 판단 반복 구조
- Python에서는 사후 판단 반복문을 제공하지 않음. ex) do~while


## GAUSS의 덧셈
- 1부터 n까지 정수의 합


    sum = n * (n + 1) // 2



## Python의 swap

    a, b = b, a

- 단일 대입문으로 swap이 가능함.
- 내부적으로 tuple을 활용함. (괄호는 생략)
- tuple로 return된 값을 각각 변수에 담을 수 있어 함수에서 여러 값을 return할 때도 tuple이 사용됨.



## _ 언더스코어

    for _ in range(n)

- _ 를 통해 필요없는 값을 무시할 수 있음.



## n개의 *를 출력하되 W개 마다 줄 바꾸는 프로그램
```
n, w = map(int, input().split())

# for i in range(n):
#     print('*', end="")
#     if i % w == w - 1:
#         print()
# if n % w:
#     print()

# for loop가 실행되는 동안 계속해서 if문의 조건을 확인 함 효율나쁨

for _ in range(n // w):
    print('*' * w) # w만큼 반복

rem = n % w
if rem: # 나머지 값이 있으면
    print('*' * rem)

# 개선 : n을 w로 나눈 만큼 반복, *은 W만큼 반복, n % W 의 나머지만큼 *을 반복
```



## Python의 난수 생성
```
import random
...
n = random.randint(1,10) # 1 <= n <= 10
```



## for~else
```
for i in range(n):
    if ~ :
        break
else: # break가 발생하지 않았을 때 동작 기술
    print('end')
```



## 드모르간 법칙
- 각 조건을 부정하고 논리곱을 논리합으로 논리합을 논리곱으로 바꾸고 다시 전체를 부정하면 원래 조건과 같음.
```
x and y == not(not x or not y)
x or y == not(not x and not y)
```


## 구조적 프로그래밍 Structured Programming
- 순차, 선택, 반복 세 종류의 제어 흐름 사용.



## Python의 변수
- Python에서는 data, function, class, module, package 등을 모두 object로 취급함.
- object [data type, memory, id(identity)]
- Python의 변수는 값을 갖지 않고 객체를 참조 함.
- immutable 속성
- 대입 연산자는 변수의 값을 복사 하는 것이 아니라 참조하므로 결합bind임.

    n = 17 # int literal 17의 id == n의 id

- 변수가 정의된 위치에 관계 없이 같은 값을 가지면 id가 같음.
- Python에서는 함수가 종료 되어도 객체가 소멸되지 않고 남아 있음. (변수의 id값 존재)


- - -

# 2장 기본 자료구조와 배열


## Array
- Python에서는 array가 없고 list와 tuple로 array를 구현함.
- empty array = return false
- 비교 연산자로 array의 대소 또는 등가 관계 판단 가능.


### List
- list는 원소를 변경할 수 있음. mutable 속성.
- 내장함수 list() 사용.
```
list1 = list('ABC') # ['A', 'B', 'C']
list2 = [None] * 5 # 원소값이 없는 크기가 5인 리스트
```


### Tuple
- tuple은 원소에 순서를 매겨 결합한 것으로 원소를 변경할 수 없음. immutable 속성.
- 내장함수 tuple()
```
tuple1 = 1,
tuple2 = (1,) # 원소가 한개인 경우 쉼표를 붙여 변수와 구분
# tuple2 = (1) <- 그냥 변수
```


### 내포 표기 생성
- list 안에서 for, if 문을 사용하여 새로운 list를 생성하는 기법. (tuple은 불가능)
```
numbers = [1,2,3,4,5]
twise = [num * 2 for num in numbers if num % 2 == 1]
# list numbers의 홀수 원소값을 *2 한 리스트 생성
# list의 element를 for문을 통해 조회하여 홀수면 2를 곱함
print(twise)
```



## Unpack
- list와 tuple을 풀어내는 것.
```
x = [1,2,3]
a, b, c = x # x를 unpack 하여 대입
# print(a,b,c) # 1,2,3
```



## Element 접근하기


### Index
- 음수 index는 0-전체원소 수 부터 1씩 증가.
- ex) 양수 0 ~ 6 , 음수 -7 ~ -1
- 존재 하지 않는 index로 접근하거나 대입해도 새로 추가 되지 않음.


### Slice
- list 나 tuple의 원소 일부를 연속해서 또는 일정한 간격으로 꺼내 새로운 list or tuple 생성.
    - s[i:j] -> s[i] ~ s[j-1] 까지 나열
    - s[i:j:k] -> s[i] ~ s[j-1]까지 k씩 step
    - i, j가 len(s)보다 커도 오류X / len(s)값으로 간주
    - i 생략 or None = 0으로 간주
    - j 생략 or None = len(s)값으로 간주
    - [:] 모두생략하면 처음부터 끝까지
    - [::-1] 맨 뒤에서부터 전부 출력(순서 반대로)



## Mutable과 Immutable의 대입
```
x = 1
y = 2
x, y = y + 1, x + 2
# 두 대입식이 동시에 이루어 지므로 x값이 업데이트 되지 않고 1로 대입
```
- mutable
    1. dictionary
    2. list
    3. set
- immutable
    1. number
    2. string
    3. tuple
```
x = 17
# statement가 아닌 expression으로 취급함
a = b = 1
# 성립되지 않음 error
```



## Annotation
- 변수나 함수 사용시 자료형에 대한 선언이 없으므로 명시적 해석을 위해 추가하는 주석.
- 파라미터 :expression / function의 return -> expression 형태로 사용.
- 주석이므로 강제적이지 않고 이와 상관없이 실행됨.
- 작성한 타입 annotation을 검사하고 싶을 때는 __annotations__내장 사전 객체 사용 
```
from typing import Any, Sequence
def max_of(a: Sequence) -> Any:
```
- Any : 제약 없는 임의의 자료형
- Sequence : list, tuple, str, bytearray, bytes



## __name__변수
- 모듈 이름을 나타내는 변수
- 프로그램이 직접 실행 될 때 __name__은 '__main __'
- 프로그램이 import 될 때 __name__은 원래 모듈 이름
- 프로그램(모듈, 파일)을 다른 파일에서 import시켜 사용하면 __name__은 '__main __'이 아니므로 해당 내용은 실행되지 않음.


