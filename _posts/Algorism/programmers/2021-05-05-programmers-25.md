---
title: "[프로그래머스] 핸드폰 번호 가리기(JAVA)"
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

> 프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.<br>
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> s는 길이 4 이상, 20이하인 문자열입니다.
<br>

## 입출력 예

|phone_number|return|
|:------|:------|
|"01033334444"|"*******4444"|
|"027778888"|"*****8888"|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public String solution(String phone_number) {
        String a = phone_number.substring(0, phone_number.length() - 4);
        a = a.replaceAll(".", "*");
        
        String back = phone_number.substring(phone_number.length() - 4);
        a = a + back;
        return a;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/117104497-32edd580-adb7-11eb-9c90-38c098f3e1f9.png)


<br>

변수 a에 매개 변수로 넘겨진 phone_number를 처음부터 총 길이의 -4한만큼 잘라서 저장했다. 그리고 `replaceAll()` 메서드로 자른 문자열의 모든 글자를 `*`로 변경했다. 그리고 phone_number의 맨 뒤 네글자를 담은 back 변수를 만들어 a에 a + back 문자열 연산을 해 a를 리턴했다.

<br><br>


**다른 사람 풀이** <br>

```java
//- , peds , - , 허영민 , - 외 45 명
class Solution {
  public String solution(String phone_number) {
     char[] ch = phone_number.toCharArray();
     for(int i = 0; i < ch.length - 4; i ++){
         ch[i] = '*';
     }
     return String.valueOf(ch);
  }
}
```

<br>

아주 간단하게 문자열을 char 배열로 넣어 for문을 돌리는 코드이다. 요즘에 계속 어렵게 생각하려고, api를 자주 사용해 보려고 하니 이렇게 간단하게 풀 수 있는 문제를 굳이 어렵게 생각해 풀이하는 것 같다.. 문제를 풀 때 조금 더 오래 생각할 시간을 가져야겠다.
