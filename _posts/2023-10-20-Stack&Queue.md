---
layout: single
title:  "[자료구조스터디] 스택 & 큐(Stack & Queue)"
categories: coding
tag: [python, blog, jekyll]
toc: true
author_profile: false
---

<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem Consolas, "Liberation Mono", Menlo, Courier, monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>


# Stack & Queue(스택과 큐)


* 스택(Stack) : 데이터를 일시적으로 보관



    1. 후입선출(LIFO : Last In First Out) : 가장 나중에 넣은 데이터를 가장 먼저 꺼냄

    2. 푸시(push) : 데이터를 넣는 작업

    3. 팝(pop) : 데이터를 꺼내는 작업



```python
# IntStack class
class OverflowIntStackException(Exception):
    def __init__(self, message="스택이 가득 찼습니다"):
        super().__init__(message)

class EmptyIntStackException(Exception):
    def __init__(self, message="스택이 비어 있습니다"):
        super().__init__(message)

class InStack:
    def __init__(self, maxlen):
        self.stk = [0] * maxlen
        self.capacity = maxlen
        self.ptr = 0

    # 스택이 비어 있는지 확인
    def is_empty(self):
        return self.ptr <= 0
    
    # 스택이 가득 찼는 지 확인
    def is_full(self):
        return self.ptr >= self.capacity
    
    # push
    def push(self, x):
        if self.is_full():
            raise OverflowIntStackException()
        self.stk[self.ptr] = x
        self.ptr += 1

    # pop
    def pop(self):
        if self.is_empty():
            raise EmptyIntStackException()
        self.ptr -= 1
        return self.stk[self.ptr]
    
    # peek
    def peek(self):
        if self.ptr <= 0:
            raise EmptyIntStackException()
        return self.stk[self.ptr - 1]
    
    # 스택의 용량을 반환
    def get_capacity(self):
        return self.capacity
    
    # 스택에 쌓여 있는 데이터 개수를 반환
    def size(self):
        return self.ptr
    
    # x의 값을 찾아 index를 반환
    def index_of(self, x):
        for i in range(self.ptr-1, -1, -1):
            if self.stk[i] == x:
                return i
        return -1
    
    # 스택 비우기
    def clear(self):
        self.ptr = 0

    # 스택 내용을 출력
    def dump(self):
        if self.is_empty():
            print("스택이 비어 있습니다")
        else:
            for i in range(self.ptr):
                print(self.stk[i], end=" ")
            print()
```


```python
# Main

def main():
    s = InStack(64)

    while True:
        print()
        print(f"현재 데이터 개수: {s.size()} / {s.get_capacity()}")
        print("(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료")

        menu = input("메뉴를 선택하세요 : ")
        if menu == "0":
            break

        x = None
        if menu in ["1", "2", "3", "4", "5"]:
            if menu == "1":
                x = int(input("데이터 : "))
                try:
                    s.push(x)
                except OverflowIntStackException as e:
                    print(e)

            elif menu == "2":
                try:
                    x = s.pop()
                    print(f"팝한 데이터는 {x}입니다")
                except EmptyIntStackException as e:
                    print(e)

            elif menu == "3":
                try:
                    x = s.peek()
                    print(f"피크에 있는 데이터는 {x}입니다")
                except EmptyIntStackException as e:
                    print(e)
            
            elif menu == "4":
                s.dump()

            elif menu == "5":
                s.clear()
        else:
            print("올바른 메뉴를 선택하세요~!")

if __name__ == "__main__":
    main()
```

<pre>

현재 데이터 개수: 0 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 1 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
올바른 메뉴를 선택하세요~!

현재 데이터 개수: 1 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 2 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 3 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 4 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
팝한 데이터는 446입니다

현재 데이터 개수: 3 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
피크에 있는 데이터는 6464입니다

현재 데이터 개수: 3 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
23 979 6464 

현재 데이터 개수: 3 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
23 979 6464 

현재 데이터 개수: 3 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 0 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료

현재 데이터 개수: 0 / 64
(1) 푸시 (2) 팝 (3) 피크 (4) 덤프 (5) 클리어 (0) 종료
</pre>
* 큐(Queue) : 일시적으로 데이터를 쌓아 놓는 자료구조



    1. 선입선출(FIFO : First In First Out) : 가장 먼저 넣은 데이터를 가장 먼저 꺼냄

    2. 인큐(en-queue) : 데이터를 넣는 작업

    3. 디큐(de-queue) : 데이터를 꺼내는 작업

    4. 프런트(front) : 데이터가 나오는 쪽

    5. 리어(rear) : 데이터를 넣는 쪽



```python
# IntQueue class
class IntQueue:
    
    class EmptyIntQueueException(Exception):
        def __init__(self, message="큐가 비어 있습니다"):
            super().__init__(message)

    class OverflowIntQueueException(Exception):
        def __init__(self, message="큐가 가득 찼습니다"):
            super().__init__(message)

    def __init__(self, maxlen):
        self.que = [0] * maxlen
        self.capacity = maxlen
        self.front = 0
        self.rear = 0
        self.num = 0

    def enque(self, x):
        if self.num >= self.capacity:
            raise self.OverflowIntQueueException()
        self.que[self.rear] = x
        self.rear = (self.rear + 1) % self.capacity
        self.num += 1
        return x
    
    def deque(self):
        if(self.num <= 0):
            raise self.EmptyIntQueueException()
        x = self.que[self.front]
        self.front = (self.front + 1) % self.capacity
        self.num -= 1
        return x
    
    def peek(self):
        if self.num <= 0:
            raise self.EmptyIntQueueException()        
        return self.que[self.front]
    
    def clear(self):
        self.num = self.front = self.rear = 0

    def index_of(self, x):
        for i in range(self.num):
            idx = (i + self.front) % self.capacity
            if(self.que[idx] == x):
                return idx            
        return -1
    
    def get_capacity(self):
        return self.capacity
    
    def size(self):
        return self.num
    
    def is_empty(self):
        return self.num <= 0
    def is_full(self):
        return self.num >= self.capacity
    
    def dump(self):
        if(self.num <= 0):
            print("큐가 비어 있습니다")

        else:
            for i in range(self.num):
                idx = (i + self.front) % self.capacity
                print(self.que[idx], end=" ")
            print()
```


```python
# main함수 작성

def main():
    q = IntQueue(64)

    while True:
        print()
        print(f"현재 데이터 개수 : {q.size()} / {q.get_capacity()}")
        print("(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료")

        menu = int(input())
        if menu == 0:
            break

        x = 0
        if menu == 1:
            print("데이터 : ")
            x = int(input())
            try:
                q.enque(x)
            except IntQueue.OverflowIntQueueException:
                print("큐가 가득 찼습니다")

        elif menu == 2:
            try:
                x = q.deque()
                print(f"디큐한 데이터는 {x}입니다")
            except IntQueue.EmptyIntQueueException:
                print("큐가 비어 있습니다")

        elif menu == 3:
            try:
                x = q.peek()
                print(f"피크한 데이터는 {x}입니다")
            except IntQueue.EmptyIntQueueException:
                print("큐가 비어 있습니다")

        elif menu == 4:
            q.dump()
            

if __name__ == "__main__":
    main()
```

<pre>

현재 데이터 개수 : 0 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
데이터 : 

현재 데이터 개수 : 1 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
데이터 : 

현재 데이터 개수 : 2 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
데이터 : 

현재 데이터 개수 : 3 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
545 949 9496 

현재 데이터 개수 : 3 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
디큐한 데이터는 545입니다

현재 데이터 개수 : 2 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
피크한 데이터는 949입니다

현재 데이터 개수 : 2 / 64
(1) 인큐 (2) 디큐 (3) 피크 (4) 덤프 (0) 종료
</pre>