---
layout: single
title:  "jupyter notebook 변환하기!"
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


# 검색 알고리즘



: 데이터 집합에서 원하는 값을 가진 요소를 찾아내는 것



1. 배열에서 검색

    1) 선형검색 : 무작위로 늘어서 있는 데이터 모임에서 검색을 수행

    2) 이진검색 : 일정한 규칙으로 늘어서 있는 데이터 모임에서 아주 빠른 검색 수행

    3) 해시법 : 추가, 삭제가 자주 일어나는 데이터 모임에서 아주 빠른 검색 수행

        - a. 체인법(오픈해시법) : 같은 해시값의 데이터를 선형 리스트로 연결하는 방법

            - <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwZ8UC%2FbtqUBvdjrtw%2FdrQoHQj6ufKwtFZXTK6CJ0%2Fimg.png">

        - b. 오픈주소법 : 데이터를 위한 해시값이 충돌할 때 재해시 하는 방법

          - <img src="https://velog.velcdn.com/images/dnrwhddk1/post/e1515905-f9e2-4751-bc37-8f090a85ee75/image.png">

  

<br>



1. 선형리스트에서 검색

   

2. 이진검색트리에서 검색



# Linear Search( 선형 검색 )



- 맨 앞에서부터 '순서대로' 검색

- 요소가 정렬되지 않은 배열에서 검색할 때 사용하는 유일한 방법



```python
def SeqSearch (arr, arrSize, key):
    print("arr = ", arr)
    print("key = ", key)
    for i in range(arrSize):
        if(arr[i] == key):
            return i
    return -1


arrSize = int(input("배열의 크기를 지정해 주세요 : "))

arr = []

for i in range(arrSize):
    arrVal = int(input("배열의 요소들을 입력해주세요("+ str(arrSize)+ "개)"))
    arr.append(arrVal)

key = int(input("검색할 값을 입력하세요 : "))

idx = SeqSearch(arr, arrSize, key)

if(idx == -1):
    print("그 값의 요소가 없습니다.")
else:
    print("그 값은 arr[" + str(idx) + "]에 있습니다.")
```

<pre>
arr =  [1, 2, 3, 4, 5]
key =  3
그 값은 arr[2]에 있습니다.
</pre>
# Binary Search( 이진 검색 )

- 데이터가 키값으로 이미 정렬(sort)되어 있다.

- 속도 : 이진검색이 선형보다 "빠름"

- 오름차순 or 내림차순 둘 다 ok

- 검색이 반복될 때마다 검색 범위가 거의 절반이 됨

    - 검색에 필요한 비교 횟수의 평균값 "log n"

        - 검색 실패 : log(n+1)회

        - 검색 성공 : log n - 1회



```python
def BinSearch(arr, arrSize, key):
    pl = 0
    pr = arrSize - 1

    while pl <= pr:
        pc = (pl + pr) / 2

        if arr[pc] < key:
            pl = pc + 1

        elif arr[pc] > key:
            pr = pc - 1

        else:
            return pc

        return -1


arrSize = int(input("배열의 크기를 지정해 주세요 : "))

arr = []

for i in range(arrSize):
    while True: 
        arrVal = int(input("arr[" + str(i) + "]"))
        if i > 0 and arrVal < arr[i - 1]:
            print("이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.")
        
        else:
            arr.append(arrVal)
            break
        

key = int(input("검색할 값을 입력하세요 : "))

idx = SeqSearch(arr, arrSize, key)

if idx == -1:
    print("그 값의 요소가 없습니다.")
else:
    print("그 값은 arr[" + str(idx) + "]에 있습니다.")
```

<pre>
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
이전 값보다 작은 값을 입력했습니다. 다시 입력하세요.
arr =  [1, 2, 3, 4, 5]
key =  6
그 값의 요소가 없습니다.
</pre>
* 복잡도(Complexity)

  1. 시간 복잡도(Time Complexity) : 실행에 필요한 시간을 평가

  2. 공간 복잡도(Space Complextity) : 기억 영역과 파일 공간이 얼마나 필요한 가를 평가한 것

     <br/>

  - 선형 검색의 시간복잡도 -> O(n)

  - 이진 검색의 시간복잡도 -> O(log n)


* Comparator & Comparable

  - 공통점

    - 객체를 비교할 수 있도록 만들어 준다

    - 용도 : 개체 정렬

    - 새로운 클래스 객체를 만들어 비교하는 경우 사용  <br/>

  - 차이점 -> 비교 대상이 다르다

    - [Comparable]

      - 자기 자신과 매개변수 객체(파라미터로 들어오는 객체)를 비교

      - lang package에 들어있음으로 따로 package를 import할 필요가 없음

      - method : compareTo(T o)

    - [Comparator]

      - 자기 자신의 상태가 어떻던 상관없이 두 매개변수 객체를 비교

      - util package에 들어 있음으로 따로 util package import가 필요

      - method : compare(T o1, T o2)

  

