---
title: "[프로그래머스] 가장 큰 정사각형 찾기(JAVA)"
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

1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)<br> 예를 들어 <br> ![문제1](https://user-images.githubusercontent.com/70805241/122673960-ff9fc280-d20d-11eb-9bfb-286f81c130e4.png) <br> 가 있다면 가장 큰 정사각형은 <br> ![문제2](https://user-images.githubusercontent.com/70805241/122673968-0f1f0b80-d20e-11eb-8d00-17022c029164.png) <br> 가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다. <br>

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 표(board)는 2차원 배열로 주어집니다.
- 표(board)의 행(row)의 크기 : 1,000 이하의 자연수
- 표(board)의 열(column)의 크기 : 1,000 이하의 자연수
- 표(board)의 값은 1또는 0으로만 이루어져 있습니다.


<br>
<br>


> ## 입출력 예

|board	|answer|
|:------|:------|
|[[0,1,1,1],[1,1,1,1],[1,1,1,1],[0,0,1,0]]|9|
|[[0,0,1,1],[1,1,1,1]]|4|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution
{
    public int solution(int [][]board)
    {   
        int x = board.length;
        int y = board[0].length;
        int max = 0;
        
        if(x <= 1 || y <= 1) return 1;
        
        for(int i = 1; i < x; i++){
            for(int j = 1; j < y; j++){
                if(board[i][j] >= 1){
                    int up = board[i-1][j];
                    int left = board[i][j-1];
                    int upperLeft = board[i-1][j-1];
                    int min = Math.min(up, left);
                    min = Math.min(min, upperLeft);
                    board[i][j] = min+1;
                    max = Math.max(max, min+1);
                }
            }
        }
        return max*max;
    }
}
```

{% endraw %}


![결과](https://user-images.githubusercontent.com/70805241/122674011-4d1c2f80-d20e-11eb-8854-b7a8231c4db2.png)

 <br>


오늘도 역시 답을 봤다. ㅎㅎ 일단 알고리즘 로직을 생각을 해보긴 했는데 구현할 능력이 부족한 것 같다. <br>
일단 생각은 역시나 완벽했다.
1. board x, y 구하기
2. 1,0 인덱스를 기준으로 위, 왼쪽, 아래가 1인지 확인하기
3. 만약 주변에 0이 있으면 기준 인덱스 변경
4. 정사각형 모양으로 1이 있으면 max에 저장
5. 또 있으면 max와 비교 후 더 큰 정사각형 크기를 저장

이렇게 생각했는데 손가락은 왜 뇌를 못따라가는지,,^^(소라게)

<br><br>

다른 사람의 코드보다는 어떤 방식으로 접근했어야 했는지를 살펴보자. <br>
먼저 내가 프로그래머스에서 제일 좋아하는 '질문하기' 버튼을 눌러 힌트를 얻고자 좀 기웃거려봤는데 어마어마한 정보를 습득했다. <br>  ![정보](https://user-images.githubusercontent.com/70805241/122674203-04b14180-d20f-11eb-9b0a-95e73ad6392a.png) <br> 정말 천사가 아닐까.. <br> 암튼 저 링크를 타고 들어가서 봤는데 오,,,, 봐도봐도 무슨 얘긴지 잘 와닿지가 않았다. 오...... ^^... 그래서 답을 찾아 소스를 분석쓰 해봤다. <br>

<br>

**정답 코드의 알고리즘 순서**
1. board 배열 x, y 축 길이 구하기
2. board가 1렬 혹은 1행으로만 올 경우 가장 큰 정사각형은 1 이 경우 조건을 따로 걸어줘야함.
3. board 1,0이 아닌^^ `(1, 1)` 기준으로 시작
4. board[i][j]가 1 이상인 경우에 위, 왼, 왼쪽 위 값 구하기
5. 위, 왼, 왼쪽 위 값의 최솟값에 +1 해주기
6. 최솟값+1을 board[i][j]에 저장
7. max = 0과 최솟값+1를 비교해 더 큰 값을 max에 저장
8. 그리고 그 다음 인덱스(1,2)의 위, 왼, 왼쪽 위 값 구하기
9. max = 1과 최솟값+1을 비교해 더 큰 값을 max에 저장
10. 반복
11. max 제곱 후 반환


<br>

나중에 따로 DP..... 정리해야겠다.....<br>