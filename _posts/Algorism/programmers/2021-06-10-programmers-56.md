---
title: "[프로그래머스] 땅따먹기(JAVA)"
excerpt: "Level 2"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_2
---


> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 1행부터 땅을 밟으며 한 행씩 내려올 때, 각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. 단, 땅따먹기 게임에는 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.<br>

예를 들면,<br>
{% raw %}
| 1 | 2 | 3 | 5 |
| 5 | 6 | 7 | 8 |
| 4 | 3 | 2 | 1 |
{% endraw %}
<br>
로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.<br>

마지막 행까지 모두 내려왔을 때, 얻을 수 있는 점수의 최대값을 return하는 solution 함수를 완성해 주세요. 위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.



<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 행의 개수 N : 100,000 이하의 자연수
- 열의 개수는 4개이고, 땅(land)은 2차원 배열로 주어집니다.
- 점수 : 100 이하의 자연수


<br>
<br>


> ## 입출력 예

|land|answer|
|:------|:------|
|[[1,2,3,5],[5,6,7,8],[4,3,2,1]]|16|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
// 틀린 코드입니다.
class Solution {
    int solution(int[][] land) {
        int answer = 0;
        int max = 0;
        int[] score = new int[4];
        int check = -1;

        for(int i = 0; i < land.length; i++){
            max = 0;
            int j;
            for(j= 0; j < land[0].length; j++){
                if(j != check && max <land[i][j]) {
                    max = land[i][j];
                }
                score[j] += max;
            }
            check = j-1; 
        }
        
        for(int n : score) {
            if(answer < n) answer = n;
        }
        
        return answer;
    }
}
```

{% endraw %}


![테스트케이스](https://blog.kakaocdn.net/dn/ebVcKl/btq6W2k2YXD/TdMH6wtMteyPWho5w1HAbk/img.png) <br>

위의 코드는 테스트 케이스는 통과했지만..^^ 코드를 제출하면 대참사가 일어나는 코드였다. <br>

![결과](https://blog.kakaocdn.net/dn/bKkoIp/btq60kEUXj5/Ec7mcKRnTfpjRVMuIeoM30/img.png) <br>

결국엔 구글링을 이용해 답을 봤다...!!!!!!!!!!

```java
import java.util.*;
class Solution {  
   public int solution(int[][] land) {
       for(int i=1; i<land.length; i++){
           land[i][0] += Math.max(Math.max(land[i-1][1], land[i-1][2]), land[i-1][3]);
           land[i][1] += Math.max(Math.max(land[i-1][0], land[i-1][2]), land[i-1][3]);
           land[i][2] += Math.max(Math.max(land[i-1][1], land[i-1][0]), land[i-1][3]);
           land[i][3] += Math.max(Math.max(land[i-1][1], land[i-1][2]), land[i-1][0]);
       }

       int[] answer = land[land.length-1];
       Arrays.sort(answer);

       return answer[answer.length-1];
   }
}
```


<br>

for문을 돌면서 i번째 행 - 1. 즉 i-1번째 행에서 해당 열 인덱스를 제외한 나머지 값들 중에서 제일 큰 값을 찾아 i번째 행렬에 더한다. 이렇게 모든 경우의 수를 더해 정렬하고 제일 큰 값을 리턴한다. <br>

![결과2](https://blog.kakaocdn.net/dn/bsFezh/btq60MHXcgz/mbqkcoJsN9rd0lojbuqS31/img.png)

<br>

구글링하면서 DP라는 단어가 나왔다. Dynamic Programming이라는데.. 나중에 따로 정리해야겠다..! 배울 건 왜 이렇게 많고 시간은 적고 나는 빈둥거리는지....
<br>