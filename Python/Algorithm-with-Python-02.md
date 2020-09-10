
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 2장 기본 자료구조와 배열

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## 문자열 리스트의 최대값
- 문자열 리스트의 최대 값은 알파벳순(오름차순)으로 가장 큰 문자코드 or 문자열을 출력



## Python의 대입
- 원소값이 같은 튜플과 리스트를 따로 생성하면 is 연산자로 identity를 비교했을때 False (서로 다른 객체를 참조)
- 같은 객체를 참조하도록 하기 위해서는
```
a = [1,2,3]
b = a
```



## List, Tuple Scan
- enumerate()사용
- enumerate() - index와 element를 tuple 형태로 return
```
for i, name in enumerate(x):
    print(f'x[{i}] = {name}')
print()
```



## Iterable 객체
- 문자열, 리스트, 튜플, 집합, 딕셔너리 등의 자료형 객체
- 반복이 가능한 iterable 객체
- 내장함수 iter() -> 객체에 대한 iterator(반복자) return
- iterator의 __next __ 함수를 호출하거나 내장함수 next()함수에 iterator를 전달하면 원소를 순차적으로 꺼낼 수 있음
- 꺼낼 원소가 더 이상 없으면 StopIteration 예외 발생



## Revers Sort
```
for i in range(n//2):
        a[i], a[n-i-1] = a[n-i-1], a[i]
```
- python 표준 라이브러리 reverse()
- mutable sequence에 한함
```
x.reverse()
y = list(reversed(x)) # x의 원소를 역순으로 정렬하여 y에 대입
```



## n진수 구하기(기수변환)
- 정수를 n진수로 변환하기 위해서는 정수를 n으로 몫이 0이 될때까지 나누고 나머지는 역순으로 정렬함
```
def card_conv(x: int, r: int) -> str :
    d = ''
    dchar = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'

    # while x > 0:
    #     d += dchar[x % r]
    #     x //= r

    n = len(str(x))
    print(f'{r:2} | {x:{n}d}')
    while x > 0:
        print('  +' + (n + 2) * '-')
        if x//r :
            print(f'{r:2} | {x//r:{n}d} ... {x%r}')
        else:
            print(f'     {x//r:{n}d} ... {x%r}')
        d += dchar [x%r]
        x //= r

    return d[::-1] #역순으로 반환
```



## Python에서의 인수 전달
- 실제 인수인 객체에 대한 참조를 값으로 전달하여 매개변수에 대입되는 방식
- call by value와 call by reference의 중간적인 참조하는 값 전달 == call by object reference
- immutable 인수 : 함수 안에서 매개변수의 값을 변경하면 다른 객체를 생성하고 그 객체에 대한 참조로 업데이트, 따라서 매개변수의 값을 변경해도 호출하는 쪽의 실제 인수에는 영향을 주지 않음
- mutable 인수 : 함수 안에서 매개변수의 값을 변경하면 객체 자체의 업데이트, 따라서 매개변수의 값을 변경하면 호출하는 쪽의 실제 인수는 값이 변경됨



## 어떤 정수 이하의 Prime number(소수)를 모두 나열하는 알고리즘
- n의 제곱근 이하의 어떤 소수로도 나누어 떨어지지 않으면 소수(약수의 대칭성)
```
cnt = 0 # 나눗셈 횟수
ptr = 0 # 이미 찾은 소수의 개수
prime = [None] * 500 # 소수를 저장하는 배열

prime[ptr] = 2
ptr += 1
prime[ptr] = 3
ptr += 1

for n in range(5, 1001, 2): # 홀수만
    i = 1
    while prime[i] * prime[i] <= n:
        cnt += 2
        if n % prime[i] == 0:
            break
        i += 1
    else:
        prime[ptr] = n
        ptr += 1
        cnt += 1
```




## List의 Element와 Copy
- 얕은 복사 : 객체가 참조 자료형의 멤버를 포함하는 경우(참조값만 복사)
    - list.copy()를 사용하면 같은 객체를 참조하므로 원소값을 변경하면 모두 변경
    - 원소 수준에서 얕은 복사 Shallow copy
- 깊은 복사 : 참조값 뿐만 아니라 참조하는 객체 자체를 복사하는 경우
    - deepcopy() in copy module
    - 구성 원소 수준까지 깊은 복사 Deep copy
    - 객체가 갖는 모든 멤버(값과 참조형식)를 복사하므로 전체 복사라고도 함
