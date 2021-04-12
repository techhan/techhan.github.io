---
title: "[프로그래머스] 나누어 떨어지는 숫자 배열(JAVA)"
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

> array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.<br>
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> arr은 자연수를 담은 배열입니다.<br>
정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.<br>
divisor는 자연수입니다.<br>
array는 길이 1 이상인 배열입니다.
<br>

## 입출력 예

|arr|divisor|return
|:------|:------||:------|
|[5, 9, 7, 10]|5|[5, 10]|
|[2, 36, 1, 3]|1|[1, 2, 3, 36]|
|[3,2,6]|10|[-1]|

<br>

## JAVA 풀이

```java
import java.util.*;

class Solution {
    public int[] solution(int[] arr, int divisor) {
        int[] answer = answer = new int[1];
        ArrayList<Integer> list = new ArrayList<>();
        
        for(int n : arr)
            if(n % divisor == 0) list.add(n);

        if(list.size() == 0) {
            answer[0] = -1;
        } else{
            answer = new int[list.size()];
            Collections.sort(list);
        
            for(int i = 0; i < list.size(); i++){
                answer[i] = list.get(i);
            }
        }
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114404578-c5e48700-9be0-11eb-8d53-ee431bc9c9e3.png)
{: width="600" height="600"}

<br>

이번 문제도 어렵지 않았다. 그리고 예전 문제고, 중간에 한 번 개편돼서 그런지 문제와 다른 코드들이 많이 보였다. 그 점을 제외하면 문제가 워낙 쉽고 간단하다 보니 비슷하게 푼 것 같다. <br>
위의 코드는 처음 제출한 코드가 아니다. 뭔가 코드를 제출하고 보니 불필요한 부분이 보여서 리팩토링했다. 하단 코드는 제출한 코드다.

```java
import java.util.*;

class Solution {
    public int[] solution(int[] arr, int divisor) {
        int[] answer = {};
        ArrayList<Integer> list = new ArrayList<>();

        for(int n : arr)
            if(n % divisor == 0) list.add(n);


        if(list.size() == 0) {
            answer = new int[1];
            answer[0] = -1;
            return answer;
        } else{
            answer = new int[list.size()];
            Collections.sort(list);

            for(int i = 0; i < list.size(); i++){
                answer[i] = list.get(i);
            }
        }
        return answer;
    }
}
```