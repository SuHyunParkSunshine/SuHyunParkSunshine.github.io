---
layout: single
title:  "[자료구조스터디] 문자열 검색"
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

# 문자열 검색
: 문자열 검색이란, 어떤 문자열 안에 특정 문자열이 들어 있는지 `조사`하고, 들어 있다면 그 위치를 찾는 것
### - 문자열 알고리즘 -
1. 브루트-포스법
2. KMP법
3. 보이어, 무어법

## 1) 브루트-포스법(Brute Force method)
- 문자열 검색의 기초
- 선형 검색을 확장한 단순한 알고리즘, (equals to 단순법, 소박법)

### 브루트-포스법으로 문자열 검색
```java
import java.util.Scanner;

public class BFmatch {

    static int bfMatch(String text, String pattern) {
        int pt = 0;     // text 커서
        int pp = 0;     // pattern 커서

        while (pt != text.length() && pp != pattern.length()) {
            if (text.charAt(pt) == pattern.charAt(pp)) {
                pt++;
                pp++;
            } else {
                pt = pt - pp + 1;
                pp = 0;
            }
        }
        if (pp == pattern.length()) {       // 검색 성공
            return pt - pp;
        }
        return -1;                          // 검색 실패
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("텍스트 : ");
        String s1 = sc.next();      // 텍스트용 문자열

        System.out.print("패 턴 : ");
        String s2 = sc.next();      // 패턴용 문자열

        int idx = bfMatch(s1, s2);  // 문자열 s1에서 문자열 s2를 검색

        if (idx == -1) {
            System.out.println("텍스트에 패턴이 없습니다.");
        } else {
            // 일치하는 문자 바로 앞까지의 문자 개수를 반각 문자로 환산하여 구함
            int len = 0;
            for (int i = 0; i < idx; i++) {
                len += s1.substring(i, i + 1).getBytes().length;
            }
            len += s2.length();

            System.out.println((idx + 1) + "번쩨 문자부터 일치합니다.");
            System.out.println("텍스트 : " + s1);
            System.out.printf(String.format("패턴 : %%%ds\n", len), s2);
        }
    }
}
// 입력값
// ABC이지스DEF
// 이지스
```
<pre>
4번쩨 문자부터 일치합니다.
텍스트 : ABC이지스DEF
패턴 :    이지스
</pre>

### String.indexOf, String.lastIndexOf 메서드로 문자열 검색
```java
import java.util.Scanner;

public class IndexOfTester {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("텍스트 : ");
        String s1 = sc.next();      // 텍스트용 문자열

        System.out.print("패 턴 : ");
        String s2 = sc.next();      // 패턴용 문자열

        int idx1 = s1.indexOf(s2);      // 문자열 s1에서 s2를 검색(앞쪽부터)
        int idx2 = s1.lastIndexOf(s2);  // 문자열 s1에서 s2를 검색(뒤쪽부터)

        if (idx1 == -1) {
            System.out.println("텍스트 안에 패턴이 없습니다.");
        } else {
            // 찾아낸 문자열 바로 앞까지의 문자 개수를 구함
            int len1 = 0;
            for (int i = 0; i < idx1; i++) {
                len1 += s1.substring(i, i + 1).getBytes().length;
            }
            len1 += s2.length();

            int len2 = 0;
            for (int i = 0; i < idx2; i++) {
                len2 += s1.substring(i, i + 1).getBytes().length;
            }
            len2 += s2.length();

            System.out.println("텍스트: " + s1);
            System.out.printf(String.format("패 턴: %%%ds\n", len1), s2);
            System.out.println("텍스트: " + s1);
            System.out.printf(String.format("패 턴: %%%ds\n", len2), s2);
        }
    }
}
// 입력값
// AB주이지스DEF이지스12
// 이지스
```
<pre>
텍스트: AB주이지스DEF이지스12
패 턴:      이지스
텍스트: AB주이지스DEF이지스12
패 턴:                  이지스
</pre>
