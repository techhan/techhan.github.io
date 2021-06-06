---
title: "[프로그래머스] 행렬의 곱셈(JAVA)"
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

2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요. 


<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
- 행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
- 곱할 수 있는 배열만 주어집니다.
<br>
<br>


> ## 입출력 예

|arr1|arr2|result|
|:------|:------|:------|
|[[1, 4], [3, 2], [4, 1]]|[[3, 3], [3, 3]]|[[15, 15], [15, 15], [15, 15]]|
|[[2, 3, 2], [4, 2, 4], [3, 1, 4]]|[[5, 4, 3], [2, 4, 1], [3, 1, 1]]|[[22, 22, 11], [36, 28, 18], [29, 20, 14]]|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr2[0].length];

        for(int  i = 0; i < arr1.length; i++){
            for(int j = 0; j < arr1[0].length; j++){
                for(int k = 0; k < arr2[0].length; k++){
                    answer[i][k] += arr1[i][j] * arr2[j][k];
                }                
            }
        }
        return answer;  
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/120892235-3e4b4f80-c648-11eb-800f-8eba480b4c86.png) <br>




<br><br>


**다른 사람의 풀이** <br>

```java
// - , - , - , - , 양5 외 13 명

// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class ProductMatrix {
    public int[][] productMatrix(int[][] A, int[][] B) {
        int[][] answer = new int[A.length][B[0].length];        
    if(A[0].length==B.length){ 
        for(int i=0; i<A.length; i++){
            for(int j=0; j<B[0].length; j++){
                for(int k=0; k<A[0].length; k++){
                  answer[i][j]+=A[i][k]*B[k][j];
                }               
            }
        }       
    }
        return answer;
    }

    public static void main(String[] args) {
        ProductMatrix c = new ProductMatrix();
        int[][] a = { { 1, 2 }, { 2, 3 } };
        int[][] b = { { 3, 4 }, { 5, 6 } };
      // 아래는 테스트로 출력해 보기 위한 코드입니다.
      System.out.println("행렬의 곱셈 : " + c.productMatrix(a, b));
    }
}
```

<br> 

다른 사람들도 거의 비슷한 로직으로 작성했다. <br>

