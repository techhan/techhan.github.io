---
title: "[프로그래머스] 약수의 개수와 덧셈(JAVA)"
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

> 두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.
 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- 1 ≤ left ≤ right ≤ 1,000


<br>

## 입출력 예

|left|right|result|
|:------|:------|:------|
|13|17|43|
|24|27|52|


<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int divisor(int num, int cnt){
        int count = 0;
        for(int i = 1; i <= num; i++){
            if(num % i == 0) count++;
        }
        return count % 2 == 0 ? 1 : 0;
    }

    public int solution(int left, int right) {
        int answer = 0;
        int[] count = new int [right-left+1];
        int cnt = 0;
        for(int i = left; i <= right; i++){
            count[cnt] = divisor(i, cnt);
            if(count[cnt] == 1) answer += i;
            else answer -= i;
            cnt++;
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/118363038-77eee480-b5cd-11eb-962e-f0dd071707fe.png)


사실 코드가 이상하게 긴 이유는 문제를 제대로 안 읽고 left에서 right까지의 숫자의 모든 약수를 더해 짝수, 홀수를 판별해서 연산하는 문제인 줄 알고 쓸데없이 count 배열을 
생성했다..^^ 문제를 제대로 읽자! ~~(사실 처음에는 2차원 배열을 선언하기도 했다..)~~<br><br>


**리팩토링**


{% raw %}

```java
class Solution {
    public int divisor(int num){
        int count = 0;
        for(int i = 1; i <= num; i++){
            if(num % i == 0) count++;
        }
        return count;
    }
    
    public int solution(int left, int right) {
        int answer = 0;
        for(int i = left; i <= right; i++){
            if(divisor(i) % 2 == 0) answer += i;
            else answer -= i;
        } 
        return answer;
    }
}
```

{% endraw %}

<br>

![결과2](https://user-images.githubusercontent.com/70805241/118363281-8f7a9d00-b5ce-11eb-91f9-c255f473e9cc.png)




<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
// 요오게
class Solution {
    public int solution(int left, int right) {
        int answer = 0;
        int s = (int)Math.ceil(Math.sqrt(left));
        int ss = s * s;
        for (int i = left; i <= right; i++) {
            if (i == ss) {
                answer -= i;
                s++;
                ss = s * s;
            } else {
                answer += i;
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

위의 코드는 Math 클래스의 함수들을 이용해 문제를 풀이했다. 