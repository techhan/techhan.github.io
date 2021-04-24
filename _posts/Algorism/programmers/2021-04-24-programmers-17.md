---
title: "[프로그래머스] 약수의 합(JAVA)"
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

> 정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n은 0 이상 3000이하인 정수입니다.
<br>

## 입출력 예

|n|return|
|:------|:------|
|12|28|
|5|6|
<br>

## JAVA 풀이 과정

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = 1; i <= n; i++){
            if(n % i == 0) answer += i;
        }
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/115964077-a42ebc80-a55d-11eb-8c30-448c844aee69.png)



<br>

처음에는 for문의 반복 개수를 줄여보고자 다음과 같은 방법을 생각했다. n의 자기 자신을 빼고 가장 큰 수는 n을 2로 나눈 값보다 작을 것 같아서 이 부분을 구현하려고 했으나, 내 머리로는 이중 for문을 돌려야 할 것 같다는 생각 밖에 안 나서 뭔가 시간 복잡도가 더 높을 것 같아서 그냥 원래 알고 있던 방법으로 풀이했다.

<br><br>

**다른 사람 풀이** <br>

```java
// - , - , 재밌는영화추천좀 , - , 이승윤 외 32 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class SumDivisor {
    public int sumDivisor(int num) {
        int answer = 0;
            for(int i = 1; i <= num/2; i++){
        if(num%i == 0) answer += i;
      }
        return answer+num;
    }

    // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String[] args) {
        SumDivisor c = new SumDivisor();
        System.out.println(c.sumDivisor(12));
    }
}
```

<br>

위의 코드가 내가 생각했던 방법을 이중 for문 없이 단일 for문으로 작성했다. for 문의 반복 조건에 `num/2`라는 방법이 있을 줄이야.. 생각도 못 했다..!

