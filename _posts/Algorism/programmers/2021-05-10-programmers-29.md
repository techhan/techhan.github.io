---
title: "[프로그래머스] 행렬의 덧셈(JAVA)"
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

> 행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. <br> 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.
<br>

## 입출력 예

|arr1|arr2|return|
|:------|:------|:------|
|[[1,2],[2,3]]|[[3,4],[5,6]]|[[4,6],[7,9]]|
|[[1],[2] ]|[[3],[4]]|[[4],[6]]|

<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr1[0].length];
        for(int i = 0; i < arr1.length; i++){
            for(int j = 0; j <arr1[0].length; j++){
              answer[i][j] = arr1[i][j] + arr2[i][j];  
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/117671014-fbc65c80-b1da-11eb-94b8-bfdbbc516f2b.png)


<br>

기본적인 문제라 딱히 말할 것이 없다!

<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
// 임성민 , - , - , 탈퇴한 사용자 , - 외 6 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class SumMatrix {
    int[][] sumMatrix(int[][] A, int[][] B) {
    int row = Math.max(A.length, B.length);
    int col = Math.max(A[0].length, B[0].length);
        //int[][] answer = {{0, 0}, {0, 0}};
    int[][] answer = new int[row][col];
    for(int i=0; i<row ; i++){
      for(int j=0; j<col; j++){
        answer[i][j] = A[i][j] + B[i][j];
      }
    }

        return answer;
    }
}
```

{% endraw %}

<br>

다른 사람의 코드도 나와 비슷한 로직으로 풀이했다. 이 코드는 변수 row와 col를 따로 선언해서 조금 더 코드가 깔끔하게 보이도록 작성하였다.