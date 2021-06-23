---
title: "[프로그래머스] 큰 수 만들기 (JAVA)"
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

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.
예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24]를 만들 수 있습니다. 이중 가장 큰 숫자는 94입니다.<br>

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.<br>


<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.


<br>
<br>


> ## 입출력 예

|number|k|return|
|:------|:------|:------|
|"1924"|2|"94"|
|"1231234"|3|"3234"|
|"4177252841"|4|"775841"|



<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public String solution(String number, int k) {
        StringBuffer answer = new StringBuffer();
        char max;
        int idx = 0;
        
        for(int i = 0; i < number.length()-k; i++){
            max = '0';
            for(int j = idx; j <= k+i; j++){
                if(max < number.charAt(j)) {
                    max = number.charAt(j);
                    idx = j + 1;
                }
            }
            answer.append(max);
        }
        return answer.toString();
    }
}
```

{% endraw %}


![결과](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc238kQ%2Fbtq7Y5UjR6M%2Fg1J6M9LDbnBkyjZqFo6Th0%2Fimg.png)

 <br>


<br><br>

**다른 사람의 풀이** <br>

```java
//김기준 , - , sabgilhun , 김준비 , RebirthLee 외 29 명
import java.util.Stack;
class Solution {
    public String solution(String number, int k) {
        char[] result = new char[number.length() - k];
        Stack<Character> stack = new Stack<>();

        for (int i=0; i<number.length(); i++) {
            char c = number.charAt(i);
            while (!stack.isEmpty() && stack.peek() < c && k-- > 0) {
                stack.pop();
            }
            stack.push(c);
        }
        for (int i=0; i<result.length; i++) {
            result[i] = stack.get(i);
        }
        return new String(result);
    }
}
```

스택을 이용해서 풀이한 코드다. 정말 놀라운 코드;;