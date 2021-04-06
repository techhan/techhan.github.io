---
title: "[프로그래머스] 두 개 뽑아서 더하기(JAVA)"
excerpt: "Level 1"
categories: 
  - Algorithm
tags: 
  - Programmers
  - Java
  - Level_1
---


## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

> 정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> numbers의 길이는 2 이상 100 이하입니다.
numbers의 모든 수는 0 이상 100 이하입니다.

<br>

## 입출력 예


|numbers|result|
|:---------:|:------:|
|[2,1,3,4,1] | [2,3,4,5,6,7] | 
|[5,0,2,7] | [2,5,7,9,12]|

<br>

## JAVA 풀이

```java
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = {};
        int idx = 0;
        ArrayList<Integer> sumArr = new ArrayList<>();
        
        for(int i = 0; i < numbers.length-1; i++){
            for(int j = 1 + i; j < numbers.length; j++){
                int temp = numbers[i] + numbers[j];
                if(sumArr.indexOf(temp) < 0){
                    sumArr.add(temp);
                }
            }
        }
        
        answer = new int[sumArr.size()];

        for(int num : sumArr){
            answer[idx++] = num;
        }
        
        Arrays.sort(answer);
        
        return answer;
    }
}
```


![결과](https://user-images.githubusercontent.com/70805241/113682824-84466e80-96fe-11eb-83cf-b50315b7bb68.png)

<br>

처음에는 오직 배열로만 풀이하려고 했다. 배열로 중복 제거까지는 생각하기 쉬웠는데 그 배열을 정렬하고... 길이를 추가하고 삭제할 생각에 메서드를 만들려다가 갑자기 ArrayList가 생각났다. ArrayList는 배열과 다른 점이 배열 길이의 추가, 삭제가 쉬워서 그리 길지 않은 코드를 작성한 것 같다. 저기서 길이를 조금 더 줄이고, 테스트 7번과 8번이 다른 테스트에 비해 느리게 나와서 코드를 바꿔보고 싶었는데 능력 부족으로 실패...!

