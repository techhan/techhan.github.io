---
title: "[프로그래머스] 최대공약수와 최소공배수(JAVA)"
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

> 두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- 두 수는 1이상 1000000이하의 자연수입니다.


<br>

## 입출력 예

|n|m|result|
|:------|:------|:------|
|3|12|[3, 12]|
|2|5|[1, 10]|



<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int gcd(int a, int b){
        if(a % b == 0) return b;
        return gcd(b, a%b);
    }
    
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        int max, min;
        
        if(n >= m) {
            max = n;
            min = m;
        } else {
            max = m;
            min = n;
        }
        
        answer[0] = gcd(max, min);
        answer[1] = max*min/answer[0];
        
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/119009507-25973480-b9ce-11eb-806d-1996884671ac.png)

<br>


이번 문제는 지금 한창 공부 중인 `재귀함수` 파트에서 봤던 `유클리드 호제법`을 이용해서 풀이했다. 

<br><br>





**다른 사람 풀이** <br>

{% raw %}

```java
//  이홍원 , - , 최영록 , - , - 외 30 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.Arrays;

class TryHelloWorld {
    public int[] gcdlcm(int a, int b) {
        int[] answer = new int[2];

          answer[0] = gcd(a,b);
        answer[1] = (a*b)/answer[0];
        return answer;
    }

   public static int gcd(int p, int q)
   {
    if (q == 0) return p;
    return gcd(q, p%q);
   }

    // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String[] args) {
        TryHelloWorld c = new TryHelloWorld();
        System.out.println(Arrays.toString(c.gcdlcm(3, 12)));
    }
}
```

{% endraw %}

<br>

다른 사람들 또한 대부분 유클리드 호제법을 사용해서 풀이했다. 이런 공식 같은 경우는 외우거나 100% 이해해서 구현할 수 있도록 연습 많이 해야겠다.