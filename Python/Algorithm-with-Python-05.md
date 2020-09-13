
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 3장 검색 알고리즘

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## Open addressing 오픈 주소법
- Collision이 발생했을 때 rehashing을 반복하여 빈 버킷을 찾는 방법
- = closed hashing 닫힌 해시법 = linear probing 선형 탐사법
```
ex) 18 % 13 = 5
table[5] 에서 Collision
rehashing (18+1) % 13 = 6
table[6] 에 추가
```

### 원소 삭제하기
- 기존 해시값을 가지는 버킷을 지워버리면 해당 해시값을 가지는 다른 데이터가 아예 존재 하지 않는다고 착각하는 오류 발생
- rehashing된 데이터를 검색할 수 없음
- 따라서 각 버킷에 속성 부여
    - 저장되어 있음(숫자)
    - 비어있음(-) : 해시값이 같은 데이터 존재하지 않음
    - 삭제완료(★) : 해시값이 같은 데이터가 다른 버킷에 존재


### 원소 검색하기
- 비어있음 : 검색실패(결과값 없음)
- 삭제완료 : rehashing하여 계속 검색


```
from __future__ import annotations
from typing import Any, Type
from enum import Enum
import hashlib

# 버킷의 속성
class Status(Enum):
    OCCUPIED = 0
    # 데이터를 저장
    EMPTY = 1
    # 비어있음
    DELETED = 2
    # 삭제완료

class Bucket:
    # 초기화
    def __init__(self, key: Any = None, value: Any = None, stat: Status = Status.EMPTY) -> None:
        self.key = key
        self.value = value
        self.stat = stat

    # 필드값 설정
    def set(self, key: Any, value: Any, stat: Status) -> None:
        self.key = key
        self.value = value
        self.stat = stat

    # 속성(=상태) 설정
    def set_status(self, stat: Status) -> None:
        self.stat = stat

class OpenHash:
    def __init__(self, capacity: int) -> None:
        self.capacity = capacity
        self.table = [Bucket()] * self.capacity
    
    def hash_value(self, key: Any) -> int:
        if isinstance(key, int):
            return key % self.capacity
        return(int(hashlib.md5(str(key).encode()).hexdigest(), 16) % self.capacity)
    
    def rehash_value(self, key: Any) -> int:
        return(self.hash_value(key) + 1) % self.capacity
    
    def search_node(self, key: Any) -> Any:
        # 키가 key인 버킷을 검색
        hash = self.hash_value(key)
        p = self.table[hash]

        for i in range(self.capacity):
            if p.stat == Status.EMPTY:
                break
            elif p.stat == Status.OCCUPIED and p.key == key:
                return p
            hash = self.rehash_value(hash)
            p = self.table[hash]
        return None
    
    def search(self, key: Any) -> Any:
        # 키가 key인 원소를 검색하여 값을 반환
        p = self.search_node(key)
        if p is not None:
            return p.value
            # 검색성공
        else:
            return None
            # 검색실패

    def add(self, key: Any, value: Any) -> bool:
        if self.search(key) is not None:
            return False
            # 이미 등록된 키
        
        hash = self.hash_value(key)
        p = self.table[hash]
        for i in range(self.capacity):
            if p.stat == Status.EMPTY or p.stat == Status.DELETED:
                self.table[hash] = Bucket(key, value, Status.OCCUPIED)
                return True
            hash = self.rehash_value(hash)
            p = self.table[hash]
        return False
        # 해시테이블이 가득참

    def remove(self, key: Any) -> int:
        p = self.search_node(key)
        if p is None:
            return False
        p.set_status(Status.DELETED)
        return True
    
    def dump(self) -> Nonde:
        for i in range(self.capacity):
            print(f'{i:2} ', end='')
            if self.table[i].stat == Status.OCCUPIED:
                print(f'{self.table[i].key} ({self.table[i].value})')
            elif self.table[i].stat == Status.EMPTY:
                print('-- 미등록 --')
            elif self.table[i].stat == Status.DELETED:
                print('-- 삭제완료 --')
```
