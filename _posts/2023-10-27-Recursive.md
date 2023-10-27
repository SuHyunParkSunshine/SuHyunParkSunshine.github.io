---
layout: single
title:  "[자료구조스터디] 재귀함수(Recursive)"
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


# 재귀(Recursive)

- 재귀적 : 어떤 사건이 자기 자신을 포함하고 있거나 또는 자기 자신을 사용하여 정의 하고 있을 때

- 사용 예시 : 팩토리얼, 유클리드 호제법(최대공약수 구하는 방법)



- 직접 재귀 : 자신과 동일한 메서드를 호출

- 간접 재귀 : a 메서드가 b를 호출, b 메서드가 다시 a 메서드를 호출


## 팩토리얼(Factorial)
```java
// 팩토리얼

import java.util.Scanner;

public class Factorial {

    class Factorial_func{
        static int factorial(int n) {
            if(n > 0)
                return n * factorial(n - 1);
            else return 1;
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("정수를 입력하세요 : ");
        int x = sc.nextInt();

        System.out.println(x + "의 팩토리얼은 " +Factorial_func.factorial(x) + "입니다.");
    }
}
```

## 유클리드 호제법(Euclidean method of mutual division)
- 최대공약수를 구하는 방법
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;

// Euclidean method of mutual division(유클리드 호제법)
// GCD(greatest common division) : 최대공약수
public class EuclidGCD {

    static int gcd(int x, int y) {
        if (y == 0) {
            return x;
        } else {
            return gcd(y, x % y);
        }
    }
    public static void main(String[] args) throws IOException {
//        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        Scanner sc = new Scanner(System.in);

        System.out.println("두 정수의 최대공약수를 구합니다");
        System.out.print("첫번째 정수를 입력하세요 : "); int x = sc.nextInt();
        System.out.print("두번째 정수를 입력하세요 : "); int y = sc.nextInt();

//        System.out.print("정수 두개를 입력하세요 : ");
//        StringTokenizer st = new StringTokenizer(br.readLine());
//        int x = Integer.parseInt(st.nextToken().split(" ")[0]);
//        int y = Integer.parseInt(st.nextToken().split(" ")[0]);

        System.out.println("최대공약수는 " + gcd(x, y) + "입니다.");
    }
}
```

## Examples of Recursive

* Recur

```java
import java.util.Scanner;

public class Recur {
    static void recur(int n) {
        if (n > 0) {
            recur(n - 1);
            System.out.println(n);
            recur(n - 2);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("정수를 입력하세요 : ");
        int x = sc.nextInt();

        recur(x);
    }
}
```
* RecurX1
```java

// recur함수 꼬리재귀(tail recursion) 제거 버전

import java.util.Scanner;

public class RecurX1 {
    static void recur_x1(int n) {
        while (n > 0) {
            recur_x1(n - 1);
            System.out.println(n);
            n = n - 2;
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("정수를 입력하세요 : ");
        int x = sc.nextInt();

        recur_x1(x);
    }
}
```
* RecurX2
```java
import Chap4_StackQueue.IntStack;

import java.util.Scanner;

// Non-recursion version -> Stack 사용!
public class RecurX2 {
    static void recur_x2(int n) {
        IntStack s = new IntStack(n);

        while (true) {
            if (n > 0) {
                s.push(n);
                n = n - 1;
                continue;
            }
            if (!s.isEmpty()) {
                n = s.pop();
                System.out.println(n);
                n = n - 2;
                continue;
            }
            break;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("정수를 입력하세요 : ");
        int x = sc.nextInt();

        recur_x2(x);
    }
}
```

## 하노이의 탑(Towers of Hanoi)
```java
import java.util.Scanner;

public class Hanoi {

    static void move(int no, int x, int y) {
        if (no > 1) {
            move(no - 1, x, 6 - x - y);
        }
        System.out.printf("원반[%d]을(를) %d번 기둥에서 %d번 기둥으로 옮김\n", no, x, y);

        if (no > 1) {
            move(no - 1, 6 - x - y, y);
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("하노이의 탑");
        System.out.print("원반의 개수 : ");
        int n = sc.nextInt();

        move(n, 1, 3);
    }
}
```
## 8-Queen
```java
// 8-Queen Problem
public class EightQueen {
    static boolean[] flag_a = new boolean[8];
    static boolean[] flag_b = new boolean[15];
    static boolean[] flag_c = new boolean[15];
    static int[] pos = new int[8];

    static void print() {
        for (int i = 0; i < 8; i++) {
            System.out.printf("%2d", pos[i]);
        }
        System.out.println();
    }

    static void setQueen(int i) {
        for (int j = 0; j < 8; j++) {
            if (!flag_a[j] && !flag_b[i + j] && !flag_c[i - j + 7]) {
                pos[i] = j;
                if (i == 7) {
                    print();
                } else {
                    flag_a[j] = flag_b[i + j] = flag_c[i - j + 7] = true;
                    setQueen(i + 1);
                    flag_a[j] = flag_b[i + j] = flag_c[i - j + 7] = false;
                }
            }
        }
    }
    public static void main(String[] args) {
        setQueen(0);
    }
}
```