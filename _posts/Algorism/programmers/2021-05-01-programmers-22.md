---
title: "[프로그래머스] 제일 작은 수 제거하기(JAVA)"
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

> 정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> arr은 길이 1 이상인 배열입니다.<br>
인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.
<br>

## 입출력 예

|arr|return|
|:------|:------|
|[4,3,2,1]|[4,3,2]|
|[10]|[-1]|

<br>

## JAVA 풀이 과정

```java
import java.util.Arrays;
import java.util.ArrayList;
class Solution {
    public int[] solution(int[] arr) {
        if(arr.length == 1) {
            arr[0] = -1;
            return arr;
        }
        int[] copyArr = arr.clone();
        Arrays.sort(copyArr);
        
        ArrayList<Integer> list = new ArrayList<>();
        
        for(int i = 0; i < copyArr.length; i++){
            if(arr[i] != copyArr[0])
                list.add(arr[i]);
        }
        
        int[] answer = new int[list.size()];
        for(int i = 0; i < list.size(); i++){
            answer[i] = list.get(i);
        }
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116785342-0b0b2300-aad4-11eb-9c62-6d7647ae53b1.png)


<br>

문제 중에 `빈 배열`인 경우를 못 보고 예시만 보고 [10]이 들어가면 바로 '-1'로 리턴하라는 줄 알고 뭐가 틀렸지;; 하면서 계속 찾고 있었다.. 문제를 다시 읽고 나서야 틀린 부분을 찾아서 고칠 수 있었다. 그리고 하나 또 간과한 건 `중복`이 있을 거라 생각도 못 했다. 테스트케이스를 돌리고 나서야 중복 처리 부분을 추가했다. <br>

코드 설명은 제일 먼저 배열의 길이가 1이면 무조건 빈 배열이 리턴될 테니 if문으로 배열의 길이가 1인 경우에 arr[0]에 `-1`을 넣어서 리턴했다. 그리고 배열의 길이가 1이 아닌 경우에는 일단 `깊은 복사`를 하기 위해 arr.clone() 메서드를 사용해서 copyArr 배열을 생성했다. 그리고 그 배열을 정렬시켜 제일 작은 수를 찾았다. 그리고 배열의 추가, 삭제를 쉽게 하기 위해 ArrayList를 선언해 for문을 돌면서 copyArr[0] 값과 arr[i]의 값이 다를 경우에 list에 arr[i] 값을 추가했다. 그리고 answer 배열을 선언해 ArrayList에 있는 값들을 옮겨 담았다.

<br><br>


**다른 사람 풀이** <br>

```java
//  RebirthLee , jysohn0825 , shcjsaud , 이재근 , 장종현 외 7 명
import java.util.Arrays;
import java.util.stream.Stream;
import java.util.List;
import java.util.ArrayList;

class Solution {
  public int[] solution(int[] arr) {
      if (arr.length <= 1) return new int[]{ -1 };
      int min = Arrays.stream(arr).min().getAsInt();
      return Arrays.stream(arr).filter(i -> i != min).toArray();
  }
}
```

<br>

위의 코드는 `stream`을 사용해서 풀이했다. 스트림을 사용하니 단 세 줄 만에 코드가 완성되는 기적을 볼 수 있었다.. 다른 코드들은 나와 비슷한 로직에 최소 값이 들어있는 `인덱스`를 구하는 코드들이 있었다. 

