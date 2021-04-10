---
title: "[프로그래머스] 체육복(JAVA)"
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

> 점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.<br><br>
전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 전체 학생의 수는 2명 이상 30명 이하입니다.<br>
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.<br>
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.<br>
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.<br>
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.
<br>

## 입출력 예

|n|lost|reserve|return
|:------|:------||:------|:------|
|5|[2, 4]|[1, 3, 5]|5|
|5|[2, 4]|[3]|4|
|3|[3]|[1]|2|

<br>

## JAVA 풀이

```java
import java.util.*;

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        n -= lost.length;
        Arrays.sort(lost);
        Arrays.sort(reserve);
        for(int i = 0; i < reserve.length; i++){
            for(int j = 0; j < lost.length; j++){
                if(reserve[i] == lost[j]){
                    reserve[i] = -1;
                    lost[j] = -1;
                    n++;
                }
            }
        }

        
        for(int i = 0; i < reserve.length; i++){
            for(int j = 0; j < lost.length; j++){
                if(lost[j] > 0) {
                    if(lost[j] -1 == reserve[i] || lost[j] +1 == reserve[i]){
                    n++;
                    lost[j] = 0;
                    reserve[i] = 0;
                     }
                }
            }
        }
        return n;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114253971-ccf47500-99e7-11eb-8da6-a68f5f746ebd.png){: width="600" height="600"}

<br>

맨 처음에 제출했을 때 12개의 테스트 케이스 중에서 3개만 통과하고 나머지는 모두 실패가 떴었다.


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
