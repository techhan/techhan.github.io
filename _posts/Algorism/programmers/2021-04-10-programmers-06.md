---
title: "[프로그래머스] 모의고사(JAVA)"
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

> 수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다. <br><br>
1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ... <br>
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ... <br>
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ... <br><br>
1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 시험은 최대 10,000 문제로 구성되어있습니다.<br>
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.<br>
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.
<br>

## 입출력 예

|answers|return|
|:------|:------|
|[1,2,3,4,5]|[1]|
|[1,3,2,4,2]|[1,2,3]|

<br>

## JAVA 풀이

```java
import java.util.*;
class Solution {
    public int[] solution(int[] answers) {
        int[] answer = {};
        int[] temp = new int[3];
        int[] cnt = new int[3];
        int[] h1 = {1, 2, 3, 4, 5};
        int[] h2 = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] h3 = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
        int idx1 = 0, idx2 = 0, idx3 = 0;
        
        for(int i = 0; i < answers.length; i++){
            if(idx1 == 5) idx1 = 0;
            if(idx2 == 8) idx2 = 0;
            if(idx3 == 10) idx3 = 0;
            
            if(answers[i] == h1[idx1++]) cnt[0]++;
            if(answers[i] == h2[idx2++]) cnt[1]++;
            if(answers[i] == h3[idx3++]) cnt[2]++;
        }
        
        for(int i = 0; i < 3; i++){
            temp[i] = cnt[i];
        }

        Arrays.sort(temp);
        ArrayList<Integer> result = new ArrayList<>();
        
        for(int i = 0; i < 3; i++){
            if(temp[2] == cnt[i]){
                result.add(i+1);
            }
        }
        
        answer = new int[result.size()];
        
       for(int i = 0; i < answer.length; i++){
           answer[i] = result.get(i);
       }
        
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114253971-ccf47500-99e7-11eb-8da6-a68f5f746ebd.png){: width="600" height="600"}

<br>

이번 문제는 코드를 작성하면 할수록 생각보다 길어져서 '이렇게 푸는 게 맞나'라는 생각이 든 문제였다. 먼저 문제의 답이 담겨있는 answers 배열의 길이만큼 for문을 돌려 수포자들이 찍은 문제들과 맞춰보고 답이 맞으면 cnt 배열에 값을 증가시킨다. 나는 cnt 배열의 값을 유지하기 위해 temp 배열에 cnt의 값을 옮겨 담고 temp을 정렬시켰다. 그리고 배열의 추가, 삭제를 쉽게 하기 위해 ArrayList인 result를 선언하고, for문을 또 돌려 정렬로 인해 제일 큰 값이 맨 마지막 인덱스에 있으니 temp[2]와 cnt[i]가 같으면 result에 i+1를 저장했다. 그리고 그걸 또 answer에 넣으려고 또 for문 사용..! 다른 사람들이 작성한 코드를 보고 내 코드를 다시 보니까 불필요한 부분이 많은 것 같다.
<br>


```java
//김기준 , 김수현 , - , - , - 외 46 명
import java.util.ArrayList;
class Solution {
    public int[] solution(int[] answer) {
        int[] a = {1, 2, 3, 4, 5};
        int[] b = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] c = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};
        int[] score = new int[3];
        for(int i=0; i<answer.length; i++) {
            if(answer[i] == a[i%a.length]) {score[0]++;}
            if(answer[i] == b[i%b.length]) {score[1]++;}
            if(answer[i] == c[i%c.length]) {score[2]++;}
        }
        int maxScore = Math.max(score[0], Math.max(score[1], score[2]));
        ArrayList<Integer> list = new ArrayList<>();
        if(maxScore == score[0]) {list.add(1);}
        if(maxScore == score[1]) {list.add(2);}
        if(maxScore == score[2]) {list.add(3);}
        return list.stream().mapToInt(i->i.intValue()).toArray();
    }
}
```

위의 코드를 보면 문제의 정답을 맞춘 개수를 구하는 코드도 훨씬 간단하고 불필요한 배열이나 변수들이 없다. 

### 참고

- [코팅팩토리_블로그](https://coding-factory.tistory.com/126)
