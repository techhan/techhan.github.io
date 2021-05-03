---
title: "[프로그래머스] 짝수와 홀수(JAVA)"
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

> 정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> num은 int 범위의 정수입니다.<br>
0은 짝수입니다.
<br>

## 입출력 예

|num|return|
|:------|:------|
|3|"Odd"|
|4|"Even"|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public String solution(int num) {
        return num % 2 == 0 ? "Even": "Odd";
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116860399-7a038b80-ac3c-11eb-92a5-b9820ba5041a.png)


<br>

별로 어려울 게 없는 기초적인 문제였다!

<br><br>


**다른 사람 풀이** <br>

```java
//  - , polar , 정명훈 , - , - 외 103 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class EvenOrOdd {
    String evenOrOdd(int num) {
        String result = "";
      if(num % 2 == 1){
        result = "Odd";
      }else{
        result = "Even";
      }
        return result;
    }

    public static void main(String[] args) {
        String str = "1 2 3 4";
        EvenOrOdd evenOrOdd = new EvenOrOdd();
        //아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println("결과 : " + evenOrOdd.evenOrOdd(3));
        System.out.println("결과 : " + evenOrOdd.evenOrOdd(2));
    }
}
```

<br>

다른 사람들의 풀이를 보면 if문을 이용해서 짝수, 홀수를 판별하는 코드가 많았다. 그 중 제일 짧고 간결한 코드!