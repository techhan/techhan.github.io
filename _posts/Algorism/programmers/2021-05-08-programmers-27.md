---
title: "[프로그래머스] 직사각형 별찍기(JAVA)"
excerpt: "Level 1"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_1
---

## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

> 이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.<br>
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n과 m은 각각 1000 이하인 자연수입니다.
<br>

## 입출력 예

**입력** <br>
{: style="margin-bottom:0px; padding-bottom:0px"}

```
5 3
```

<br>

**출력** <br>
{: style="margin-bottom:0px; padding-bottom:0px"}

```
*****
*****
*****
```

<br>

## JAVA 풀이 과정

```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        for(int i = 0; i < b; i++){
            for(int j = 0; j < a; j++){
                System.out.print("*");
            }
            System.out.println("");
        }
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/117542042-71022800-b049-11eb-8e16-710297a46887.png)

<br>

처음보는 유형에 조금 당황했긴 했지만, 너무나도 기초적인 문제이기 때문에 딱히 할 말이 없다!

<br><br>


**다른 사람 풀이** <br>

```java
// - , paul-kim , - , wade , Dahun Kang 외 2 명
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        StringBuilder sb = new StringBuilder();
        for(int i=0; i<a; i++){
            sb.append("*");
        }
        for(int i=0; i<b; i++){
            System.out.println(sb.toString());
        }
    }
}
```

<br>

나와 같이 풀이한 유형이 제일 많았고, 그 다음에 제일 눈에 띄었던 건 `StringBuilder()` 클래스를 이용한 코드였다. 또 아는 문제다보니 습관적으로 `System.out.print()` 함수로 풀어버렸다..! StringBuilder를 잊지말자.