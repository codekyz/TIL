
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 3장 검색 알고리즘

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## Hashing 해시법
- 검색 뿐 아니라 추가, 삭제도 효율적으로 수행
- index를 연산을 통해 구함. 구해진 값 = hash value(=digest)
- hash table : hash value를 index로 하여 원소를 새로 저장한 배열
- bucket : hash table에서 만들어진 원소(데이터가 없으면 None을 가짐)
- hash function : key -> hash value 변환


### Collision 해시 충돌
- index가 중복(Bucket이 중복)되는 현상
```
ex)
table[5] -> 5인 상황에서
18을 추가하려고 할때 hash value는 5이기 때문에
18또한 table[5]에 저장되어야 함
```
- key와 hash value는 일반적으로 n:1
- 충돌을 해결하는 방법 : 체인법 / 오픈주소법



## Chaining 체인법 (= open hashing)
- hash value가 같은 원소를 linked list로 관리
- 각 bucket은 'hash value가 같은 노드를 연결한 리스트'의 head node를 참조

```
from __future__ import annotations
from typing import Any, Type
import hashlib

class Node:
    # 해시를 구성하는 노드(bucket)
    def __init__(self, key: Any, value: Any, next: Node) -> Node:
        # 초기화
        self.key = key
        self.value = value
        self.next = next
        # 뒤쪽 노드 참조

class ChainedHash:
    # 체인법으로 해시 클래스 구현
    def __init__(self, capacity: int) -> None:
        # 초기화
        self.capacity = capacity
        # 해시 테이블 크기
        self.table = [None] * self.capacity
        # 해시 테이블 선언

    def hash_value(self, key: Any) -> int:
        # 해시값을 구함
        if isinstance(key, int): # key가 int형인 경우
            return key % self.capacity
            # key를 capacity로 나눈 나머지를 해시값으로
        return(int(hashlib.sha256(str(key).encode()).hexdigest(), 16) % self.capacity)
        # key가 int형이 아닌 경우(문자열, 리스트, 클래스 등)
        # 표준 라이브러리로 형 변환 후 해시값 얻음
        # sha256 알고리즘 : hashlib제공, RSA의 FIPS 알고리즘 바탕, 주어진 byte문자열의 해시값을 구하는 해시 알고리즘의 생성자
        # encode() : key를 str형으로 변환한뒤 encode()함수를 통해 byte문자열 생성
        # hexdigest() : 해시값을 16진수 문자열로 꺼냄
        # int() : 꺼낸 문자열을 int형으로 변환
    
    def search(self, key: Any) -> Any:
        hash = self.hash_value(key)
        # 검색하는 키의 해시값
        p = self.table[hash]
        # 노드를 주목

        while p is not None:
            if p.key == key:
                return p.value
                # 검색성공
            p = p.next
            # 뒤쪽 노드 주목

        return None
        # 검색실패

    def add(self, key: Any, value: Any) -> bool:
        hash = self.hash_value(key)
        p = self.table[hash]

        while p is not None:
            if p.key == key:
                return False
                # 추가 실패
            p = p.next
            # 뒤쪽 노드 주목
        
        temp = Node(key, value, self.table[hash])
        self.table[hash] = temp
        # 노드 추가
        return True
        # 추가 성공

    def remove(self, key: Any) -> bool:
        hash = self.hash_value(key)
        p = self.table[hash]
        pp = None
        # 바로 앞 노드 주목

        while p is not None:
            if p.key == key:
                if pp is None:
                    self.table[hash] = p.next
                else:
                    pp.next = p.next
                return True
            pp = p
            p = p.next
        return False
    
    def dump(self) -> None:
        for i in range(self.capacity):
            p = self.table[i]
            print(i, end='')
            while p is not None:
                print(f'    -> {p.key} ({p.value})', end='')
                p = p.next
            print()
            # 모든 원소를 덤프하는 함수
```



## Hash function 해시 함수
- 해시 충돌이 전혀 발생하지 않는다면 해시 함수로 index를 찾는것 만으로 대부분 작업이 완료되므로 시간 복잡도는 O(1)
- 충돌을 억제하려면 hash table의 크기가 커야하는데 이는 메모리 낭비
- 시간과 공간의 trade off 상충 관계 문제가 발생

### Division Method 나눗셈 법
- 데이터를 hash table의 크기로 나누고 그 나머지를 hash value로 사용
- 어떤 값이든 테이블의 크기로 나누면 그 나머지는 절대 테이블의 크기를 넘지 않음(0 ~ n-1 주소 반환 보장)
- hash table의 크기는 prime number를 선호함
    - 충돌을 피하려면 hash table의 크기보다 작거나 같은 정수를 고르게 생성해야함


### Digit Folding 자릿수 접기
- 숫자의 각 자릿수를 더해 해시 값을 만드는 것
- 문자열을 키로 사용하는 hash table에 잘 어울림