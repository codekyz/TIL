
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 3장 검색 알고리즘

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## 배열 검색
- 선형 검색 Linear Search
- 이진 검색 Binary Search
- 해시법 Hash
    - 체인법
    - 오픈주소법



## 선형 검색 Linear Search
- key값을 가진 원소를 찾을 때 까지 순서대로 검색하는 알고리즘
- 정렬되지 않은 배열에서 사용
- 종료 조건
    - 검색 성공 : key값을 가진 원소 찾음
    - 검색 실패 : 원소를 찾지 못하고 배열의 맨 끝을 지나침
- 배열 원소가 n개 일때 조건을 판단하는 횟수 = 평균 n/2번
```
def seq_search_f(a: Sequence, key: Any) -> int:
    for i in range(len(a)):
        if a[i] == key:
            return i
    return -1
```



## 보초법 Sentinel Method
- Linear Search를 반복할 때 마다 2가지 종료조건을 체크하는데 드는 cost를 반으로 줄이기 위한 방법
- 배열의 맨 끝에 보초 key를 추가하여 무조건 key값을 찾고 종료하도록 하고 찾은 원소가 배열의 원래 데이터인지 보초인지 판단 하여 return
- if문의 판단횟수는 반으로 줄고 보초인지 판단하는 과정으로 수행이 1번 늘어남
```
def seq_search(seq: Sequence, key: Any) -> int:
    a = copy.deepcopy(seq) # seq 복사
    a.append(key) # 보초 key를 추가

    i = 0
    while True:
        if a[i] == key:
            break # 검색성공 while 종료
        # 반복을 종료하기 위해 판단하는 횟수가 절반으로 줄어듬
        i += 1
    return -1 if i == len(seq) else i
    # if condition one-liner
```




## 이진 검색 Binary Search
- 오름차순이나 내림차순으로 sort된 배열에서 효율적인 알고리즘
- 선형 검색보다 빠름
- 종료 조건
    - 검색 성공 : a[pc]와 key가 일치하는 경우
    - 검색 실패 : 검색 범위가 더 이상 없는 경우
```
from typing import Any, Sequence

def bin_search(a: Sequence, key: Any) -> int:
    pl = 0
    pr = len(a)-1

    while True:
        pc = (pl+pr) // 2
        if a[pc] == key:
            return pc
        elif a[pc] < key:
            pl = pc + 1
        else:
            pr = pc - 1
        if pl > pr:
            break
    # return -1
    raise ValueError
    # 예외 처리

if __name__ == '__main__':
    num = int(input('원소 수 입력 : '))
    x = [None] * num

    print('데이터를 오름차순으로 입력하세요')

    x[0] = int(input('x[0] : '))

    for i in range(1, num):
        while True:
            x[i] = int(input(f'x[{i}] : '))
            if x[i] >= x[i-1]:
                break

    ky = int(input('검색할 원소 입력 : '))

    try:
        idx = bin_search(x, ky)
    except ValueError:
        print('검색 실패')
    # 예외처리
    else:
        print(f'검색 성공 : x[{idx}]')
```
- 반복할때 마다 검색범위가 거의 절반으로 줄어드므로 필요 비교 횟수는 평균 log n
    - 실패할 경우 |log(n+1)| (|x| : x의 천장함수 ceiling function, x보다 크거나 같은 정수 가운데 가장 작은 수)
    - 성공할 경우 log n -1




## 복잡도 Complexity
- 알고리즘의 성능을 객관적으로 평가하는 기준
    - 시간 복잡도 time complexity
    - 공간 복잡도 space complexity
- 선형 검색 알고리즘의 시간복잡도 : O(n)
- 이진 검색 알고리즘의 시간복잡도 : O(log n)



## index()
```
obj.index(x, i, j)
```
- obj[i:j]에서 x와 같은 원소를 찾아서 가장 작은 index return
- 없으면 예외처리로 ValueError return


