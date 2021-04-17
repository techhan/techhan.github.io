---
title: "[프로그래머스] 문자열 내 p와 y의 개수(JAVA)"
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

> 대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.<br><br>예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 문자열 s의 길이 : 50 이하의 자연수<br>
문자열 s는 알파벳으로만 이루어져 있습니다.
<br>

## 입출력 예

|s|answer|
|:------|:------|
|"pPoooyY"|true|
|"Pyy"|false|


<br>

## JAVA 풀이 과정

```java
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        int yc = 0;  int pc = 0;
        for(int i = 0; i < s.length(); i++){
            if(s.toLowerCase().charAt(i) == 'y') yc++;
            else if(s.toLowerCase().charAt(i) == 'p') pc++;
        }
       
        if(yc != pc) answer = false;

        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/115112436-89d66b00-9fc0-11eb-98e5-ea9b1a417f2c.png)
{: width="600" height="600"}

<br>

이번 문제는 `toLowerCase()` 메서드 덕분에 조금 버벅거렸지만 그래도 저번 문제보다는 엄~청 쉬운 편이었다. 일단 y와 p의 개수를 세는 변수 두 개를 선언하고, for문을 s 문자열의 길이만큼 돌리면서 s 문자열의 모든 알파벳을 `toLowerCase()`로 소문자를 만들고, y와 p를 찾으면 각각의 카운트 변수에 +1을 증가시켰다. 그리고 마지막으로 for문을 빠져나와 y의 개수와 p의 개수가 같지 않으면 answer에 false 값을 넣어 리턴했다.



<br><br>




**다른 사람 풀이** <br>
```java
// aispark , - , 신영환 , - , - 외 12 명
class Solution {
    boolean solution(String s) {
        s = s.toUpperCase();

        return s.chars().filter( e -> 'P'== e).count() == s.chars().filter( e -> 'Y'== e).count();
    }
}
```

<br>

처음에 코드를 보고 정말 당황했다. 난생처음 보는 화살표와 filter 메서드.. 댓글들을 읽어보니 `람다식`이라고 한다. 이것이 자바다 목차에서 언뜻 본 기억이 나는데,, 그 부분을 읽어보진 않았다..! 공부할게 하나 더 늘었다. 공부는 해도 해도 끝이 없네.