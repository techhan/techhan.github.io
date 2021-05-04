---
title: "[프로그래머스] 정수 제곱근 판별(JAVA)"
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

> 임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.<br>
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> n은 1이상, 50000000000000 이하인 양의 정수입니다.
<br>

## 입출력 예

|n|return|
|:------|:------|
|121|144|
|3|-1|

<br>

## JAVA 풀이 과정

```java
import java.lang.Math;
class Solution {
    public long solution(long n) {
        long answer = (long)Math.sqrt(n);
        if(answer * answer == n) answer = (answer+=1) * answer;
        else answer = -1;
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116983008-8521ee80-ad04-11eb-9ab7-ae07f4da3ad1.png)


<br>

제곱근이라는 단어를 봤을 때 예전에 사용했었던 `Math.sqrt()` 메서드가 떠올랐다. Math.sqrt() 메서드는 반환값이 double 타입으로 반환되어서 메서드 앞에 `(long)`을 붙여주어 형 변환을 해 answer 변수에 담았다. 그리고 answer * answer 했을 때 매개 변수로 주어지는 n 값과 같으면 (answer + 1)의 제곱을 리턴하고, n과 값이 다르면 -1을 리턴하는 코드를 작성했다.

<br><br>


**다른 사람 풀이** <br>

```java
class Solution {
  public long solution(long n) {
      if (Math.pow((int)Math.sqrt(n), 2) == n) {
            return (long) Math.pow(Math.sqrt(n) + 1, 2);
        }

        return -1;
  }
}
```

<br>

이 풀이는 `Math.pow()` 메서드까지 사용해 코드를 아주 간결하게 짰다. Math.pow() 메서드는 지정된 숫자의 거듭제곱을 계산할 수 있다. 왜 Math.sqrt() 메서드만 생각했는지..! Math.pow() 메서드도 잊지 말자.