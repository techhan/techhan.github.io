---
title: "[프로그래머스] 다음 큰 숫자(JAVA)"
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

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.

예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.<br>

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- n은 1,000,000 이하의 자연수 입니다.
<br>
<br>


> ## 입출력 예

|n|answer|
|:------|:------|
|78|83|
|15|23|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        String nStr = Integer.toBinaryString(n);
        int nCnt = 0;

        for(int i = 0; i < nStr.length(); i++){
            if(nStr.charAt(i) == '1') nCnt++; 
         }
        
        for(int i = n+1; ; i++){
            String temp = Integer.toBinaryString(i);
            int nextNumCnt = 0;
            for(int j = 0; j < temp.length(); j++){
                if(temp.charAt(j) == '1') nextNumCnt++; 
            }
            
            if(nextNumCnt == nCnt) {
                answer = i;
                break;
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/121024928-a2544c00-c7df-11eb-9dab-d497c01fa9c3.png)

 <br>





<br><br>


**다른 사람의 풀이** <br>

```java
// - , -
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.lang.Integer;

class TryHelloWorld
{
    public int nextBigNumber(int n)
    {
      int a = Integer.bitCount(n);
      int compare = n+1;

      while(true) {
        if(Integer.bitCount(compare)==a)
          break;
        compare++;
      }

      return compare;
    }

    public static void main(String[] args)
    {
        TryHelloWorld test = new TryHelloWorld();
        int n = 78;
        System.out.println(test.nextBigNumber(n));
    }
}
```

<br> 

위의 방법은 `Integer.bitCount()` 메서드를 사용해 짧고 간단하게 풀이했다. Integer.bitCount(x) 메서드는 x의 숫자를 2진수로 변환 후 `1`의 수를 반환하는 함수이다. 

