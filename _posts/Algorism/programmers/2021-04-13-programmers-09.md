---
title: "[프로그래머스] 두 정수 사이의 합(JAVA)"
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

> 두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.<br>
a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.<br>
a와 b의 대소관계는 정해져있지 않습니다.
<br>

## 입출력 예

|a|b|return|
|:------|:------||:------|
|3|5|12|
|3|3|3|
|5|3|12|

<br>

## JAVA 풀이

```java
import java.util.*;
class Solution {
    public long solution(int a, int b) {
        long answer = 0;
        int max = Math.max(a, b);
        int min = Math.min(a, b);
        
        for(int i = min; i <= max; i++){
            answer+=i;
        }
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114496082-2c59bb80-9c5a-11eb-95a3-f8fabcf5175e.png)
{: width="600" height="600"}

<br>

이번 문제는 매개변수로 주어지는 a와 b의 대소 관계를 먼저 따진 후, 작은 값부터 큰 값까지의 합을 구하는 문제다. 처음에는 if문을 이용해서 대소 관계를 구할까 했는데 저번에 배운 `Math.max`([포스팅](https://techhan.github.io/algorithm/programmers-06/))가 생각나서 Math.max와 Math.min 메서드를 사용했다.


**다른 사람 풀이** <br>
```java
// 박철우 , - , - , 이수빈 , suebinmon 외 24 명
class Solution {

    public long solution(int a, int b) {
        return sumAtoB(Math.min(a, b), Math.max(b, a));
    }

    private long sumAtoB(long a, long b) {
        return (b - a + 1) * (a + b) / 2;
    }
}

// aerain , - , ChoEunhyun , - , 고귀한 외 4 명
class Solution {
  public long solution(int a, int b) {
      long answer = 0;
      for (int i = ((a < b) ? a : b); i <= ((a < b) ? b : a); i++) 
          answer += i;

      return answer;
  }
}
```

첫 번째 코드는 정말 생각지도 못한 코드였다. 등차수열의 합 공식인데 이걸 몰랐던 나는 수학을 처음부터 다시 공부해야 하나 보다.... 두 번째 코드는 삼 항 연산자를 이용해서 대소 관계를 for 문 조건문에서 구했다. 세상엔 천재가 많다. 나는 아니지만!