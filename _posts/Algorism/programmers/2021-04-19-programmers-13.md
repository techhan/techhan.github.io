---
title: "[프로그래머스] 서울에서 김서방 찾기(JAVA)"
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

> String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요. seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> seoul은 길이 1 이상, 1000 이하인 배열입니다.<br>
seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.<br>
"Kim"은 반드시 seoul 안에 포함되어 있습니다
<br>

## 입출력 예

|seoul|return|
|:------|:------|
|["Jane", "Kim"]|"김서방은 1에 있다"|

<br>

## JAVA 풀이 과정

**첫 번째 풀이** <br>

```java
class Solution {
    public String solution(String[] seoul) {
        String answer = "";

        for(int i = 0; i < seoul.length; i++){
            if(seoul[i].equals("Kim")){
                answer = "김서방은 " + i + "에 있다";
                break;
            }
        }
        
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/115238474-af967800-a158-11eb-886d-625ff1d69e8d.png)



<br>

처음에는 그렇게 깊게 생각하지 않고 바로 떠오르는 for문으로 풀었다. seoul 배열을 for문으로 돌려 Kim과 똑같은 배열을 찾으면 그 인덱스를 answer에 담아 리턴했다.



<br><br>

**두 번째 풀이** <br>

```java
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
    public String solution(String[] seoul) {
        ArrayList<String> list = new ArrayList<>(Arrays.asList(seoul));
        return "김서방은 " + list.indexOf("Kim") + "에 있다";
    }
}
```
<br>

![결과](https://user-images.githubusercontent.com/70805241/115234118-a525af80-a153-11eb-9c88-770d5beebe4b.png) <br>

간단한 문제라 뭔가 아쉬워서 조금 리팩토링해봤다. 일단 seoul 배열 값들을 담은 ArrayList를 만들고 `indexOf` 메서드를 사용해서 바로 리턴 시켜주었다. 

<br><br>

**다른 사람 풀이** <br>

다른 사람의 풀이를 보는데 두 번째 풀이와 비슷하게 푼 코드를 봤다. 댓글들이 많이 달렸는데 `indexOf`의 효율성에 대한 얘기가 많이 나왔다. 이 문제에서는 굳이 `ArrayList`를 생성해 메모리 할당할 필요 없이 배열 자체를 for문을 돌려 푸는 게 더 낫다는 반응이 많았다. 두 코드의 결과를 보면 속도적인 측면에서는 비슷비슷한 것 같지만 메모리 공간을 생각하면 확실히 그냥 for문으로만 풀어도 충분한 것 같다. 
