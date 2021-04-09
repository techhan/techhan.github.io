---
title: "[프로그래머스] 가운데 글자 가져오기(JAVA)"
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

> 단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> s는 길이가 1 이상, 100이하인 스트링입니다.
<br>

## 입출력 예

|s|return|
|:------|:------|
|"abcde"|"c"|
|"qwer"|"we"|

<br>

## JAVA 풀이

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        int l = s.length();
        int m = l / 2;
        if(l % 2 == 0){
            for(int i = m-1; i <= m; i++){
                answer += s.charAt(i) + "";
            }
        }else{
           answer = s.charAt(m) + "";
        }
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114179589-2625bf80-997a-11eb-9ed4-18dab039853f.png)

<br>

이번 문제도 그렇게 어려운 난이도는 아니라 별 막힘없이 풀 수 있었다. 충격이었던 건 또 다른 사람의 코드였다. 나는 대략 10줄이 넘게 코드를 짰는데, 이 문제를 단 한 줄로 풀었다.

```java
// - , - , 이석곤 , - , - 외 42 명
class StringExercise{
    String getMiddle(String word){

        return word.substring((word.length()-1) / 2, word.length()/2 + 1);    
    }
    // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void  main(String[] args){
        StringExercise se = new StringExercise();
        System.out.println(se.getMiddle("power"));
    }
}
```

`subString`이란 메서드의 존재는 알고 있었으나 워낙 메서드를 이용해 알고리즘을 풀어본 적이 별로 없어서 문제를 풀 때는 떠올리지 못했다. subString 메서드를 사용하면 매개변수로 넘어온 word의 길이가 짝수인지, 홀수인지 구하지 않아도 된다. subString은 `String.substring(start)` 이런 식으로 사용하면 start 위치부터 문자열 끝까지를 자르고, 위의 코드와 같이 `String.substring(start, end)` 이런 식으로 매개 변수를 두 개 작성하면 start 위치부터 end `전`까지의 문자열을 반환한다.


### 참고

- [코팅팩토리_블로그](https://coding-factory.tistory.com/126)
