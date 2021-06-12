---
title: "[프로그래머스] 짝지어 제거하기(JAVA)"
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

짝지어 제거하기는, 알파벳 소문자로 이루어진 문자열을 가지고 시작합니다. 먼저 문자열에서 같은 알파벳이 2개 붙어 있는 짝을 찾습니다. 그다음, 그 둘을 제거한 뒤, 앞뒤로 문자열을 이어 붙입니다. 이 과정을 반복해서 문자열을 모두 제거한다면 짝지어 제거하기가 종료됩니다. 문자열 S가 주어졌을 때, 짝지어 제거하기를 성공적으로 수행할 수 있는지 반환하는 함수를 완성해 주세요. 성공적으로 수행할 수 있으면 1을, 아닐 경우 0을 리턴해주면 됩니다<br>

예를 들어, 문자열 S = baabaa 라면<br>
b aa baa → bb aa → aa →
<br>
의 순서로 문자열을 모두 제거할 수 있으므로 1을 반환합니다.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 문자열의 길이 : 1,000,000이하의 자연수
- 문자열은 모두 소문자로 이루어져 있습니다.


<br>
<br>


> ## 입출력 예

|s|result|
|:------|:------|
|baabaa|1|
|cdcd|0|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.Stack;

class Solution
{
    public int solution(String s)
    {
        int answer = -1;
        Stack<Character> stk = new Stack<>();
        
        stk.push(s.charAt(0));
        for(int i = 1; i < s.length(); i++){
            if(!stk.isEmpty() &&stk.peek() == s.charAt(i)) stk.pop();
            else stk.push(s.charAt(i));
        }
        return stk.isEmpty() ? 1 : 0;
    }
}
```

{% endraw %}


![결과](https://user-images.githubusercontent.com/70805241/121772213-ff207f80-cbae-11eb-8a5f-f27f5839c0a2.png) <br>

문제는 레벨1에 있던 카카오 개발자 겨울 인턴십 문제인 크레인 인형뽑기 게임과 비슷해서 생각보다 금방 풀 수 있던 문제였다.

<br><br>

**다른 사람의 풀이** <br>

```java
//  - , 임재훈 , -
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.Stack;

class Solution
{
    public int solution(String s)
    {

        byte[] bytes = s.getBytes();
        int length = bytes.length;

        Stack<Integer> stack = new Stack<>();

        int iLeft = 0, iRight = iLeft + 1;
        for (; iLeft < length && iRight < length; ) {
            if (bytes[iLeft] == bytes[iRight]) {
                // bytes[iLeft] = 0;
                // bytes[iRight] = 0;

                if (stack.empty()) {
                    /*
                    while (iLeft >= 0 && bytes[iLeft] == 0) iLeft--;
                    while (iRight < length && bytes[iRight] == 0) iRight++;

                    if (iLeft < 0) iLeft = iRight;
                    if (iRight <= iLeft) iRight = iLeft + 1;
                    */

                    iLeft = iRight + 1;
                    iRight = iLeft + 1;
                } else {
                    iLeft = stack.pop();
                    iRight++;
                }
            } else {
                stack.push(iLeft);

                iLeft = iRight;
                iRight = iLeft + 1;
            }
        }

        return iLeft >= length && iRight >= length ? 1 : 0;
    }
}
```

1바이트 문자열에 쓸 수 있는 방법으로 풀이한 코드다.<br><br>

