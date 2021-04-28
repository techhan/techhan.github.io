---
title: "[프로그래머스] 자릿수 더하기(JAVA)"
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

> 자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요. <br>
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> N의 범위 : 100,000,000 이하의 자연수
<br>

## 입출력 예

|N|return|
|:------|:------|
|123|6|
|987|24|

<br>

## JAVA 풀이 과정

```java
public class Solution {
    public int solution(int n) {
        int answer = 0;
        while(n > 0){
            answer = answer + (n%10);
            n = n/10;
        }
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116370610-85724380-a845-11eb-8297-fef66179a33c.png)


<br>

사실 어제 풀었던 [문제](https://techhan.github.io/algorithm/programmers-19/)와 별로 다를게 없는 문제라 시간이 오래 걸리진 않았다. 
<br><br>


**다른 사람 풀이** <br>

```java
//  - , 김수현

import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;

        while(true){
            answer+=n%10;
            if(n<10)
                break;

            n=n/10;
        }

        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("Hello Java");

        return answer;
    }
}
```

<br>

다른 사람의 풀이는 대부분 내 코드와 비슷한 로직이다.


