---
title: "[프로그래머스] 정수 내림차순으로 배치하기(JAVA)"
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

> 함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n은 1이상 8000000000 이하인 자연수입니다.
<br>

## 입출력 예

|N|return|
|:------|:------|
|118372|873211|

<br>

## JAVA 풀이 과정

```java
import java.util.Arrays;
class Solution {
    public long solution(long n) {
        long answer = 0;
        String nStr = n + "";
        char[] nArr = nStr.toCharArray();
        Arrays.sort(nArr);
        StringBuilder nBui = new StringBuilder();
        nBui.append(nArr).reverse().toString();
        answer = Long.parseLong(nBui.toString());
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116677078-bcca2700-a9e2-11eb-896f-9045c5d5a0fe.png)


<br>

저번에 풀었던 [자연수 뒤집어 배열로 만들기](https://techhan.github.io/algorithm/programmers-19/) 이 문제에서 정렬 부분만 추가된 거라 금방 풀 줄 알았는데 의외로 '내림차순'이 나를 당황하게 했다. Arrays.sort로는 내림차순을 할 수가 없어서 이것저것 찾아보던 중 [이 문제](https://techhan.github.io/algorithm/programmers-14/)에서 다른 사람 풀이에 StringBuilder를 거꾸로 출력한 코드가 떠올라서 이런 식으로 풀이했다. 일단 매개 변수 n을 String 타입인 nStr로 만들고, nStr로 char 타입인 배열 nArr를 만들었다. 그리고 오름차순으로 nArr를 정렬하고, StringBuilder인 nBui를 선언해 오름차순으로 정렬이 된 nArr를 거꾸로(반대로) 담아 내림차순을 만들었다. 그리고 Int 타입이 아닌 Long 타입이므로 Integer.parseInt 말고 `Long.parseLong`으로 바꾸어주었다.

<br><br>


**다른 사람 풀이** <br>

```java
// -
import java.util.*;

class Solution {
  public long solution(long n) {
        String[] list = String.valueOf(n).split("");
        Arrays.sort(list);

        StringBuilder sb = new StringBuilder();
        for (String aList : list) sb.append(aList);

        return Long.parseLong(sb.reverse().toString());
  }
}
```

<br>

다른 사람의 풀이는 람다식을 사용해서 한 줄로 코드를 끝내신 분도 있었지만 나는 이 분의 풀이가 제일 보기 좋아 보인다. 나랑 똑같은 로직이라 그럴 수도 있지만.... 나는 언제쯤 answer 변수를 꼭 써야 한다는 강박감에서 벗어날 수 있을까~!

