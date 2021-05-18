---
title: "[프로그래머스] x만큼 간격이 있는 n개의 숫자(JAVA)"
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

> 함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.


<br>

## 입출력 예

|x|n|result|
|:------|:------|:------|
|2|5|[2,4,6,8,10]|
|4|3|[4,8,12]|
|-4|2|[-4, -8]|


<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        long num = x;
        for(int i = 0; i < answer.length; i++){
            answer[i] = num;
            num += x;
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/118686943-7298d080-b83f-11eb-930c-1487e142d755.png)




어려운 문제가 아니라 따로 설명하지 않아도 될 것 같다. 그냥 조금 신경 써야하는 건 num의 자료형을 `int`가 아닌 `long`으로 해야한다. int로 했더니 테스트 케이스 13, 14번이 실패로 떴었다.

<br><br>





**다른 사람 풀이** <br>

{% raw %}

```java
// - , SJH , 유상빈 , William Son , 김연욱 외 3 명
import java.util.*;
class Solution {
    public static long[] solution(int x, int n) {
        long[] answer = new long[n];
        answer[0] = x;

        for (int i = 1; i < n; i++) {
            answer[i] = answer[i - 1] + x;
        }

        return answer;

    }
}
```

{% endraw %}

<br>

위의 코드는 answer[0]에 x 값을 넣은 후 for문을 돌려서 answer[i-1]한 값에 x를 더하는 방법으로 풀이했다. 놀랍구먼,,