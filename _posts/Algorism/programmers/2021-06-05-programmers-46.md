---
title: "[프로그래머스] 피보나치 수(JAVA)"
excerpt: "Level 2"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_2
---


> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다. <br>

예를들어
- F(2) = F(0) + F(1) = 0 + 1 = 1
- F(3) = F(1) + F(2) = 1 + 1 = 2
- F(4) = F(2) + F(3) = 1 + 2 = 3
- F(5) = F(3) + F(4) = 2 + 3 = 5
<br>

와 같이 이어집니다. <br>

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.


<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- n은 1이상, 100000이하인 자연수입니다.
<br>
<br>


> ## 입출력 예

|n|result|
|:------|:------|
|3|2|
|5|5|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        if(n == 1 || n == 0) return 1;
        int a = 0;
        int b = 1;

        for(int i = 2; i <= n; i++){
            answer = (a+b) % 1234567;
            a = b;
            b = answer;
        }
        return   answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/120826011-f3243480-c594-11eb-9390-839d98abab8f.png) <br>


이번 문제에서는 n이 1일 경우와 0일 경우를 주의하면서 풀면 금방 풀 수 있을 것 같다.  <br>



<br><br>


**다른 사람의 풀이** <br>

```java
// - , 이주현 , 장동혁

// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class Fibonacci {
    public long fibonacci(int num) {
        long answer = 0;
    long[] dp = new long[num+1];
    dp[0]=0;dp[1]=1;

    for(int i = 2 ; i<=num;i++){
      dp[i] = dp[i-1]+dp[i-2];
    }

        return dp[num];
    }

  // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String[] args) {
        Fibonacci c = new Fibonacci();
        int testCase = 3;
        System.out.println(c.fibonacci(testCase));
    }
}
```

<br> 

위 방법은 배열을 이용해서 풀이했다. <br>

