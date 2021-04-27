---
title: "[프로그래머스] 자연수 뒤집어 배열로 만들기(JAVA)"
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

> 자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n은 10,000,000,000이하인 자연수입니다.
<br>

## 입출력 예

|n|return|
|:------|:------|
|12345|[5,4,3,2,1]|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public int[] solution(long n) {
        String num = n + "";
        char[] numArr = num.toCharArray();
        int[] answer = new int[numArr.length];
        int idx = 0;
        for(int i = numArr.length-1; i >=0; i--){
            answer[idx++] = numArr[i] -'0';
        }
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116230597-ccebc780-a792-11eb-975f-9301e81754d5.png)


<br>

문제를 보고 처음에 딱 든 생각은 `거스름돈`이었다. 거스름돈을 구했었던 로직으로 풀어볼까 했는데 조금 다른 방식으로 풀어보고 싶어서 생각을 좀 많이 해봤다. <br>
일단 매개변수 n을 String 타입으로 만들고, 그 String 변수를 char 배열에 담았다. 그리고 for문으로 char 배열 뒷부분부터 answer 배열에 대입했다.
<br><br>


**다른 사람 풀이** <br>

```java
// 조성민 , 이문열 , 이해니 , - , 윤인식 외 6 명

class Solution {
  public int[] solution(long n) {
      String a = "" + n;
        int[] answer = new int[a.length()];
        int cnt=0;

        while(n>0) {
            answer[cnt]=(int)(n%10);
            n/=10;
            System.out.println(n);
            cnt++;
        }
      return answer;
  }
}
```

<br>

위의 코드는 String 변수 a를 단순히 answer 배열의 크기를 구하는 데에만 사용했다. 그 이후 코드는 거스름돈 로직과 똑같다!


