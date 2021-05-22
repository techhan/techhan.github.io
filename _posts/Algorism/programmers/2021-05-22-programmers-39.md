---
title: "[프로그래머스] 소수 찾기(JAVA)"
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

> 1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.<br>
소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.
(1은 소수가 아닙니다.)

 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- n은 2이상 1000000이하의 자연수입니다.


<br>

## 입출력 예

|n|result|
|:------|:------|
|10|4|
|5|3|



<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int n) {
        int cnt = 0;
        if(n == 2) return 1;
        int[] prime = new int[n/2+1];
        prime[cnt++] = 2;
        prime[cnt++] = 3;
        for(int i = 5; i <= n; i+=2){
            boolean flag = false;
            for(int j = 1; prime[j]*prime[j] <= i; j++){
                if(i % prime[j] == 0){
                    flag = true;
                    break;
                }
            }
            if(!flag){
                prime[cnt++] = i;
            }
        }
        return cnt;
    }
}
```

{% endraw %}

<br>


![결과](https://user-images.githubusercontent.com/70805241/119200206-6b83f380-bac7-11eb-9397-33f3866794fe.png)

<br>


이번 문제는 제곱근을 이용해서 풀이했다. 일단 prime 배열을 생성해 0번째 인덱스에 2, 1번째 인덱스에 3을 대입했다. 그리고 for문을 돌려 i는 5부터 시작, 반복은 i가 n보다 같거나 작을때까지 반복한다. 그리고 짝수는 제외하기 위해 i에 2씩 누적 저장한다. 그리고 안쪽 for문에서는 제곱근을 이용해 prime[j]* prime[j]이 i보다 작거나 같으면 for문을 실행하고, 만약 i보다 크면 for문을 돌지 않고 바로 prime 배열에 i 값을 추가한다. 만약 안쪽 for문에 진입할 수 있는 조건이면 i를 prime 배열에 있는 소수와 나누어 만약 나누어 떨어지면 밑의 if(!flag)를 실행하지 못하게 flag를 true로 대입하고 break로 for문을 빠져나온다.

<br><br>

다른 사람의 풀이보다는 `에라토스테네스의 체`라는 방식이 다른 사람들의 풀이 중 댓글에 보여서 이 부분에 대해 찾아봤다. 찾아보니 내가 작성한 코드와 비슷한 부분이 많아서 좀 당황스러웠다. 공부했던 책에서는 설명만 있을 뿐 방식의 명칭은 안 알려줬어서....


## 에라토스테네스의 체

방법은 아래와 같다. 

<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif
" height="400px" width="400px">
</p>


1. 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
2. 2는 소수이므로 오른쪽에 2를 쓴다. (빨간색)
3. 자기 자신을 제외한 2의 배수를 모두 지운다.
4. 남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다.(초륵색)
5. 자기 자신을 제외한 3의 배수를 모두 지운다.
6. 남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다.(파란색)
7. 자기 자신을 제외한 5의 배수를 모두 지운다.
8. 남아있는 수 가운데 7은 소수이므로 오른쪽에 7을 쓴다.(노란색)
9. 자기 자신을 제외한 7의 배수를 모두 지운다.
10. 위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다.

<br>

그림의 경우 **11<sup>2</sup> > 120**이므로 11보다 작은 수의 배수들만 지워도 충분하다. 즉, 120보다 작거나 같은 수 가운데 2, 3, 5, 7의 배수를 지우고 남는 수는 모두 소수이다.

<br><br>

```java
class Solution {
    public int solution(int n) {
        int count = 0;
        int[] arr = new int[n+1];
        arr[0] = arr[1] = 0;

        // 배열에 값 넣기
        for(int i = 2; i <= n; i++) arr[i] = i;
        
        for(int i = 2; i <= (int)Math.sqrt(n); i++){
            if(arr[i] == 0) continue;
            for(int j = i + i; j <= n; j += i) arr[j] = 0;
        }
        
        for(int i = 0; i < arr.length; i++){
            if(arr[i] != 0) count++;
        }
        return count;
    }
}
```



![결과2](https://user-images.githubusercontent.com/70805241/119211174-1ce45280-bae3-11eb-968a-85cd08361248.png)

<br>

arr 길이가 n+1인 이유는 배열 참조 번호와 소수가 일치하도록 배열의 크기를 n+1개만큼 길이를 할당했다. 즉, 인덱스 번호 0과 1은 사용하지 않는다. 그렇기 때문에 밑의 for문에서도 i가 2부터 시작한다. <br>

for문에서는 정수 배열 2부터 시작한다. n의 제곱근만큼 반복문을 돌리며 해당 수(i)와 배수(j)는 소수가 아니먄 값을 0으로 바꾼다. <br>

그리고 마지막 for문에서 arr 배열을 검사하면서 0이 아닌 배열의 숫자를 세 반환하면 된다.


