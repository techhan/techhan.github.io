---
title: "[프로그래머스] 3진법 뒤집기(JAVA)"
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

> 자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.


 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- n은 1 이상 100,000,000 이하인 자연수입니다.


<br>

## 입출력 예

|n|result|
|:------|:------|
|45|7|
|125|229|


<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int n) {
        StringBuffer sb = new StringBuffer();
        while(n > 0){
            sb.append(n % 3);
            n = n / 3;
        }
        return Integer.parseInt(sb.toString(), 3);
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/118405950-b7d8c900-b6ac-11eb-9245-74a8bec61b83.png)


문제 제목에 '진법'이 들어가면 뭔가 부담이 생기는 것 같다. 그래서 미루고 미뤘다가 이제서야 풀게 되었는데 생각보다 어렵지 않았고, 코드도 짧았다. 'n진법'에 겁먹지 말자. 코드 설명을 해보면 일단 문자열 연산 부분이 필요해 StringBuffer 클래스를 선택했다. 그리고 while문에서 n을 3진법으로 변환하는데, sb에 쌓이는 순서가 3진법이 뒤바뀐 순서로 저장되어 굳이 따로 `reverse()`를 하지 않아도 됐다. 그래서 바로 sb를 10진법으로 변환해 리턴했다.

<br><br>





**다른 사람 풀이** <br>

{% raw %}

```java
// 민윤기 , 김태현 , 김학송
class Solution {
    public int solution(int n) {
        int answer = 0;
        String third = Integer.toString(n, 3);
        StringBuffer sb = new StringBuffer(third);
        String reversed = sb.reverse().toString();

        int exp = 0;
        for (int i = reversed.length() - 1; i >= 0; i--) {
            answer += Integer.parseInt(String.valueOf(reversed.charAt(i))) * Math.pow(3, exp);
            exp++;
        }

        return answer;
    }
}
```

{% endraw %}

<br>

위의 코드는 String과 StringBuffer를 섞어 사용했고,for문을 이용해서 3진법인 reversed를 10진법으로 변환해 answer에 담아 리턴했다.