---
title: "[프로그래머스] 숫자의 표현(JAVA)"
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

Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.

- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- n은 10,000 이하의 자연수 입니다.
<br>
<br>


> ## 입출력 예

|n|answer|
|:------|:------|
|15|4|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int n) {
        int answer = 1;
        int num = 1;
        int sum = 0;
        int check = 1;
        while(num <= n){
            if(sum == n){
                answer++; 
                sum = 0;
                num = ++check;
            } else if(sum > n){
                num = ++check;
                sum = 0;
            }
            sum += num++;
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/120934547-acbc0a80-c739-11eb-8463-38b4e8b19cf6.png)

 <br>





<br><br>


**다른 사람의 풀이** <br>

```java
// - , - , - , 이수정 , 즈스크 외 4 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class Expressions {

    public int expressions(int num) {
        int answer = 0;
        for (int i = 1; i <= num; i += 2) {
            if (num % i == 0) {
                answer++;
            }
        }
        return answer;
    }

    public static void main(String args[]) {
        Expressions expressions = new Expressions();
        // 아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println(expressions.expressions(15));
    }
}

```

<br> 

어떤 방법을 이용한 건지는 정확히 모르겠지만 댓글에 친절하게 설명해주신 분들이 있었다.<br>  ![댓글](https://user-images.githubusercontent.com/70805241/120934992-b7779f00-c73b-11eb-8e5e-3521b025f77d.png) <br>
바로 이 댓글이었는데 음... 뭐가 됐든 연속 된 자연 수 문제가 나오면 위의 방법처럼 풀어야겠다. <br> 

