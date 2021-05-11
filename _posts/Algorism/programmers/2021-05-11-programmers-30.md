---
title: "[프로그래머스] 콜라츠 추측(JAVA)"
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

> 1937년 Collatz란 사람에 의해 제기된 이 추측은, 주어진 수가 1이 될때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다. <br>

```
1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.
```

예를 들어, 입력된 수가 6이라면 6→3→10→5→16→8→4→2→1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야하는지 반환하는 함수, solution을 완성해 주세요. 단, 작업을 500번을 반복해도 1이 되지 않는다면 –1을 반환해 주세요.<br>

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 입력된 수, num은 1 이상 8000000 미만인 정수입니다.
<br>

## 입출력 예

|n|return|
|:------|:------|
|6|8|
|16|4|
|626331|-1|

<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int num) {
        long number = num;
        int answer;
        for(answer = 0; answer < 500; answer++){
            if(number == 1) return answer;
            else{
                if(number % 2 == 0) number /= 2;
                else number = number * 3 + 1;
            }
        } 
        return -1;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/117811833-a00bda00-b293-11eb-8f75-6643d2d8b1d1.png)


<br>

처음에 코드 실행을 했었을 때 계속 `테스트 3`번이 '-1'이 리턴되지 않고 488이 리턴되었다. 그래서 syso를 찍어보니 매개변수 num으로 들어오는 값은 int 타입으로 표현할 수 있는 값이 들어오지만, 연산을 하다보면 int 타입을 넘어서는 범위의 값이 나와서 계속 `488`이 나오는 것이었다. 그래서 처음에 num 값을 long 타입인 number에 대입했고, number로 연산을 수행하니 정상적으로 `-1`를 리턴했다.

<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
// - , - , - , - , - 외 6 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class Collatz {
    public int collatz(int num) {
    long n = (long)num;
    for(int i =0; i<500; i++){      
      if(n==1) return i;
      n = (n%2==0) ? n/2 : n*3+1;            
    }
    return -1;
  }
    // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String[] args) {
        Collatz c = new Collatz();
        int ex = 6;
        System.out.println(c.collatz(ex));
    }
}
```

{% endraw %}

<br>

이 코드는 나와 비슷한 로직인데 짝수, 홀수를 구해 연산을 하는 부분을 `삼항 연산자`로 풀이해 더 깔끔하게 보인다. if와 else 부분이 간단한 부분에는 삼항 연산자를 꼭 쓰자!