
> Do it! 자료구조와 함께 배우는 알고리즘 입문 (파이썬편)

- - -


# 4장 스택과 큐

*학습하면서 새로 알게된, 이해하는데 시간이 오래 걸린 부분 위주로 정리함*


## Stack
- 데이터를 임시 저장할 때 사용하는 자료구조
- LIFO 후입선출
    - top : push, pop이 이루어지는 윗부분
    - bottom : 아랫부분

### 고정 길이 스택 클래스 FixedStack 구현
- ptr : stack pointer
    - FixedStack의 ptr : ptr <= 0(empty), ptr >= capacity(full)

```
from typing import Any

class FixedStack:
    class Empty(Exception):
        pass
        # 비어있는 FixedStack에 팦 또는 피크할 때 내보내는 예외처리

    class Full(Exception):
        pass
        # 가득 찬 FixedStack에 푸시할 때 내보내는 예외처리

    def __init__(self, capacity: int = 256) -> None:
        self.stk = [None] * capacity
        self.capacity = capacity
        self.ptr = 0

    def __len__(self) -> int:
        return self.ptr
        # 데이터 개수 반환 ptr 값을 그대로 반환
    
    def is_empty(self) -> bool:
        return self.ptr <= 0
    
    def is_full(self) -> bool:
        return self.ptr >= self.capacity

    def push(self, value: Any) -> None:
        if self.is_full():
            raise FixedStack.Full # 예외 처리 발생
        self.stk[self.ptr] = value 
        self.ptr += 1

    def pop(self) -> Any:
        if self.is_empty():
            raise FixedStack.Empty # 예외 처리 발생
        self.ptr -= 1
        return self.stk[self.ptr]

    def peek(self) -> Any:
        if self.is_empty():
            raise FixedStack.Empty # 예외 처리 발생
        return self.stk[self.ptr - 1]

    def clear(self) -> None:
        self.ptr = 0

    def find(self, value: Any) -> Any:
        for i in range(self.ptr - 1, -1, -1):
            if self.stk[i] == value:
                return i
        return -1
    
    def count(self, value: Any) -> bool:
        c = 0
        for i in range(self.ptr):
            if self.stk[i] == value:
                c += 1
        return c

    def __contains__(self, value: Any) -> bool:
        return self.count(value)

    def dump(self) -> None:
        if self.is_empty():
            print('스택 비어있음')
        else:
            print(self.stk[:self.ptr])
```
- push() : value를 stk[ptr]에 저장하고 ptr 1 증가
- pop() : ptr 1 감소시키고 str[ptr]에 저장된 값을 반환, 값을 아예 꺼냄
- peek() : top data of stack, pop()할 수 있는 데이터, stk[ptr-1] 반환
- find() : top에서 bottom으로 선형검색(ptr -> 0)
- __contains __() : membership test operator인 in을 사용하여 x in stk로도 수행 가능



## Special Method
- Python 내부적으로 이미 만들어진 메소드
- Magic Method, Dunder(double underscore) Method
<https://docs.python.org/3/reference/datamodel.html#special-method-names>


## 예외 처리의 기본 구조
```
# try 문
try:
    원래 처리
except:
    예외 포착과 처리(1개 이상)
else:
    예외가 포착 되지 않음(생략가능)
finally:
    마무리(생략가능)

# try-finally 문
try:
    원래 처리
finally:
    예외 포착과 관계없이 실행
```

### raise문을 이용한 의도적 예외 처리
- 표준 내장 예외 처리
    - ValueError Class, ZeroDivisionError Class 등 파이썬이 제공
    - BaseException Class와 직간접적으로 파생한 클래스로 제공
- 사용자 정의 예외 처리
    - Exception Class에서 파생하는 것이 원칙
