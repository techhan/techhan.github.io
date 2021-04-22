---
title: "[프로그래머스] 수박수박수박수박수박수?(JAVA)"
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

> 길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n은 길이 10,000이하인 자연수입니다.
<br>

## 입출력 예

|n|return|
|:------|:------|
|3|"수박수"|
|4|"수박수박"|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public String solution(int n) {
        String answer = "";
        for(int i = 1; i <= n; i++){
            if(i % 2 != 0) answer += "수";
            else answer += "박";
        }
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/115717312-06988900-a3b5-11eb-8bdd-b7821598dfda.png)




<br>

어렵지 않은 문제였다. 나의 문제점은 이런 문제를 보면 '그저 쉽게만' 풀이하려고 하는 것 같다. 코드를 줄일 생각이 나 메서드를 사용하지 않고 '와 내가 풀 수 있는 문제다.'하면서 냉큼 풀어버린다..! 좀 더 생각을 하면서 푸는 연습을 꼭 해야 할 것 같다. <br>
코드는 간단하다. for문을 n만큼 돌려 if문으로 홀, 짝을 판별하고 홀수이면 '수', 짝수이면 '박'을 answer에 누적 저장했다. 여기서 String과 StringBuilder, 혹은 StringBuffer를 알고 있었음에도 불구하고 String을 써버린 나는..! ㅎㅎ 연습하자 생각 연습.




<br><br>

**다른 사람 풀이** <br>

```java
// - , 장봉기 , - , 장재진 , - 외 2 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class WaterMelon {
    public String watermelon(int n){

        return new String(new char [n/2+1]).replace("\0", "수박").substring(0,n);
    }

    // 실행을 위한 테스트코드입니다.
    public static void  main(String[] args){
        WaterMelon wm = new WaterMelon();
        System.out.println("n이 3인 경우: " + wm.watermelon(3));
        System.out.println("n이 4인 경우: " + wm.watermelon(4));
    }
}
```

<br>

이 코드를 보고는 놀라움을 금치 못했다. 나는 저 문제 하나 풀려고 무려 10줄이나 되는 코드를 작성했는데, 이 코드는 단 4줄로 문제를 풀어버린다. 천재란.. 이런 것일까..? ㅎㅎ 물론 코드가 짧다고 다 좋은 건 아니지만 항상 코드를 짧게 짜려고 노력하고, 생각하는 사람들이 신기하게 느껴진다. 나도 언젠가 저렇게 짤 수 있기를....!
간략하게 설명하면 char 빈 배열을 n/2+1 만큼 선언한다. 그럼 빈 배열 안에는 초깃값인 `\0`이 들어 있을 테니 그 부분을 `replace()` 함수를 통해 "수박"으로 변경한다. 그러고 나서 `substring()`으로 처음부터 n까지 잘라내어 리턴한다.

