---
title: "[프로그래머스] 주식가격(JAVA)"
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

초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.


<br>
<br>


> ## 입출력 예

|prices|return|
|:------|:------|
|[1, 2, 3, 2, 3]|[4, 3, 1, 1, 0]|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        int sec = 0;
        for(int i = 0; i < prices.length; i++){
            sec = 0;
            for(int j = i+1; j < prices.length; j++){
                sec++;
                answer[i] = sec;
                if(prices[i] > prices[j]) break;
            }
        }
        return answer;
    }
}
```

{% endraw %}


![결과](https://user-images.githubusercontent.com/70805241/122067625-b0811880-ce2e-11eb-94c3-98f0a1ccd9a5.png) <br>

스택/큐보다 배열로 더 빨리 풀이할 것 같아 배열로 풀이했다. 초를 세는 변수 sec를 선언하고 prices의 길이만큼 반복을 돌린다. 첫 번째 for문에서는 0번부터, 두 번째 for문에서는 i+1번부터 시작한다. 즉 prices[i]가 1이라면 prices[j]는 2, 3, 2, 3까지 반복한다. prices[i]가 prices[j]보다 클 때 break로 for문을 빠져나오도록 했다. 굳이 sec 변수 없이 answer[i]++;로 해도 됐었지만 보기 편하게 sec 변수를 선언했다. sec 변수가 없는 코드는 아래와 같다. <br>

```java
class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        for(int i = 0; i < prices.length; i++){
            for(int j = i+1; j < prices.length; j++){
                answer[i]++;
                if(prices[i] > prices[j]) break;
            }
        }
        return answer;
    }
}
```

<br><br>

**다른 사람의 풀이(스택)** <br>

```java
// - , - , - , - , 이하섭 외 7 명
import java.util.Stack;

class Solution {
    public int[] solution(int[] prices) {
        Stack<Integer> beginIdxs = new Stack<>();
        int i=0;
        int[] terms = new int[prices.length];

        beginIdxs.push(i);
        for (i=1; i<prices.length; i++) {
            while (!beginIdxs.empty() && prices[i] < prices[beginIdxs.peek()]) {
                int beginIdx = beginIdxs.pop();
                terms[beginIdx] = i - beginIdx;
            }
            beginIdxs.push(i);
        }
        while (!beginIdxs.empty()) {
            int beginIdx = beginIdxs.pop();
            terms[beginIdx] = i - beginIdx - 1;
        }

        return terms;
    }
}
```

