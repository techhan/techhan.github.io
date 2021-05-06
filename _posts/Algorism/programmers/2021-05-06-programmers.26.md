---
title: "[프로그래머스] 평균 구하기(JAVA)"
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

> 정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> arr은 길이 1 이상, 100 이하인 배열입니다.<br>
arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.
<br>

## 입출력 예

|arr|return|
|:------|:------|
|[1,2,3,4]|2.5|
|[5,5]|5|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public double solution(int[] arr) {
        double answer = 0;
        for(int n : arr){
            answer += n;
        }
        return answer / arr.length;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/117309873-d0333180-aebd-11eb-996f-4ea36ff45990.png)


<br>

너무나도 기초적인 문제이기 때문에 딱히 할 말이 없다!

<br><br>


**다른 사람 풀이** <br>

```java
// - , 덱스또 , 이태훈 , - , 탈퇴한 사용자 외 21 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.Arrays;

public class GetMean {
    public int getMean(int[] array) {
        return (int) Arrays.stream(array).average().orElse(0);
    }

    public static void main(String[] args) {
        int x[] = {5, 4, 3};
        GetMean getMean = new GetMean();
        // 아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println("평균값 : " + getMean.getMean(x));
    }
}
```

<br>

위의 코드는 `스트림`으로 풀이한 코드인데 댓글로 사람마다 의견이 분분했다. 짧아서 놀라운 코드이고, 처음 보는 메서드를 볼 수 있어서 좋았지만 이렇게 라이브러리 말고 알고리즘을 이용해서 푸는 방법이 효율성이 더 높다고 한다. 그래도 효율성을 차치하더라도 이런 코드를 볼 수 있다는 것이 정말 좋은 기회인 것 같다.
