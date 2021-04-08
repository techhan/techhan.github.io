---
title: "[프로그래머스] K번째 수(JAVA)"
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

> 배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다. <br>예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면 <br>
1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다. 

>배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> array의 길이는 1 이상 100 이하입니다.<br>
array의 각 원소는 1 이상 100 이하입니다.<br>
commands의 길이는 1 이상 50 이하입니다.<br>
commands의 각 원소는 길이가 3입니다.<br>


<br>

## 입출력 예


|array|commands|return|
|:---------|:------|:------|
|[1, 5, 2, 6, 3, 7, 4]|[[2, 5, 3], [4, 4, 1], [1, 7, 3]]|[5, 6, 3]|


<br>

## JAVA 풀이

```java
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
       
        for(int i = 0; i < commands.length; i++){
             ArrayList<Integer> temp = new ArrayList<>();
            for(int j = commands[i][0] - 1; j < commands[i][1]; j++){
                temp.add(array[j]);
            }
            Collections.sort(temp);
            answer[i] = temp.get(commands[i][2] - 1);
        }
        return answer;
    }
}
```


![결과](https://user-images.githubusercontent.com/70805241/113895764-3f0c6480-9804-11eb-97cc-83c8fe35dbc2.png)

<br>

문제 자체가 그렇게 어렵지 않아서 코드 작성은 금방 했는데 테스트 케이스에서 자꾸 이상하게 통과가 되지 않았다.
![테스트](https://user-images.githubusercontent.com/70805241/113944952-5c5f2400-9840-11eb-8e57-154b3c1f46f7.png)<Br>
answer의 0 번째 인덱스는 잘 나오는데 1, 2번째 인덱스 값이 틀리게 나와서 for문의 조건식을 수정해봐도 답이 없길래 한 줄씩 천천히 찾아보니 temp을 for문 밖에다가 선언해서 첫 번째 commands 배열이 다 돌고 나서 temp에 계속 값이 덮어 씌워졌던 게 문제였다..! 그래도 이번 문제는 조금 빠르게 푼 것 같아서 뿌듯하다.