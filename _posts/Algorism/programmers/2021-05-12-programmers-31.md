---
title: "[프로그래머스] 음양 더하기(JAVA)"
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

> 어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다. 실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 
- bsolutes의 길이는 1 이상 1,000 이하입니다.
    - absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
- signs의 길이는 absolutes의 길이와 같습니다.
    - signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.

<br>

## 입출력 예

|absolutes|signs|result|
|:------|:------|:------|
|[4,7,12]|[true,false,true]|9|
|[1,2,3]|[false,false,true]|0|

<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;
        for(int i = 0; i < absolutes.length; i++){
            if(!signs[i]) absolutes[i] *= -1;
            answer += absolutes[i];
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/117993251-24348f00-b372-11eb-910b-27e8e6443703.png)



<br>

문제가 약간 길어서 어려울 것 같아 긴장했지만 막상 읽어보니 그리 어려운 문제는 아니였다. for 문을 돌려서 signs[i]값이 `false`면 absolutes[i] 에 있는 값에 `absolutes[i] *= -1`를 해주어 양수를 음수로 바꾸고 answer에 누적 저장했다.

<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
// 김정수 , yohanjang , Danbi Choi , 요오게 , 김지석 외 7 명
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;
        for (int i=0; i<signs.length; i++)
            answer += absolutes[i] * (signs[i]? 1: -1);
        return answer;
    }
}
```

{% endraw %}

<br>

`삼항 연산자`로 코드를 간단하게 작성했다. 이놈의 삼항연산자는 문제 풀 때 왜 이렇게 안 떠오를까.... 아무튼 깔끔하고 좋은 코드다!