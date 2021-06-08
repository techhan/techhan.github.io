---
title: "[프로그래머스] 올바른 괄호(JAVA)"
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

괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

- "()()" 또는 "(())()" 는 올바른 괄호입니다.
- ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.

'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 문자열 s의 길이 : 100,000 이하의 자연수
- 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.
<br>
<br>


> ## 입출력 예

|s|answer|
|:------|:------|
|"()()"|true|
|"(())()"|true|
|")()("|false|
|"(()("|false|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.Stack;

class Solution {
    boolean solution(String s) {
        Stack<Character> stk = new Stack<>();
        
        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) == '(') stk.push(s.charAt(i));
            if(stk.isEmpty()) return false;
            if(s.charAt(i) == ')') stk.pop();
        }
        
        
        return stk.isEmpty() ? true : false;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/121185496-19054e00-c8a1-11eb-953e-d06b9985a291.png)


 <br>

이번 문제는 자료구조 중 `스택(Stack)`을 이용해서 풀이했다. 매개 변수로 받은 문자열 s의 길이만큼 for문을 돌린다. 첫 번째 if문에서는 s의 한 글자가 '('면 스택에 저장한다. 그리고 두 번째 if에서 만약 스택이 비어있으면 첫 번째의 한 글자가 ')'이므로 올바른 괄호가 아니니 바로 false를 리턴해줬다. 그리고 세 번째 if문에서는 s의 한 글자가 ')'이면 스택에서 값을 빼내었다. 그래서 맨 마지막 return 문에 스택이 비어있으면 올바른 문자이니 삼항연산자를 이용해 비어있으면 true, 아니면 false를 리턴하도록 했다.



<br><br>


**다른 사람의 풀이** <br>

```java
// - , - , 재현 , 김수현 , 최진영 외 2 명
class Solution {
    boolean solution(String s) {
        boolean answer = false;
        int count = 0;
        for(int i = 0; i<s.length();i++){
            if(s.charAt(i) == '('){
                count++;
            }
            if(s.charAt(i) == ')'){
                count--;
            }
            if(count < 0){
                break;
            }
        }
        if(count == 0){
            answer = true;
        }

        return answer;
    }
}
```

<br> 

위의 방법은 스택을 쓰지 않고 구현했다.
