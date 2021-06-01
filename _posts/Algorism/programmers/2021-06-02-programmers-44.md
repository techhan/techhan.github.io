---
title: "[프로그래머스] N개의 최소공배수(JAVA)"
excerpt: "Level 1"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_1
---


> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

<br>

> ## 입출력 예

|arr|result|
|:------|:------|
|[2,6,8,14]|168|
|[1,2,3]|6|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int solution(int[] arr) {
        int max = arr[0]; 
        
        for(int n : arr){
            if(max < n) max = n;
        }
        
        for(int i = 1; ; i++){
            int temp = max * i;
            boolean flag = true;
            for(int j = 0; j < arr.length; j++){
                if(temp % arr[j] != 0) {
                    flag = false;
                    break;
                }
            }
            if(flag) return temp;
        }
    }
}
```

{% endraw %}

<br>


![결과](https://user-images.githubusercontent.com/70805241/120356048-e27a8100-c33e-11eb-9297-5aec391e7847.png)



<br>

일단 배열 값 중에 제일 큰 값을 구했다. 그리고 for문을 돌리면서 max에 담긴 값에 1..2..3.. 이렇게 곱한 값을 temp에 넣고 안쪽 for문에서 temp을 arr[j]로 나누었을 때 0이 되지 않으면 flag에 false를 대입하고 안쪽 for문을 종료했다. 이렇게 계속 반복시키다 안쪽 for문을 돌려도 flag가 true로 유지되면 temp 값을 리턴시켰다. <br>


<br><br>


**다른 사람의 풀이** <br>

```java
// 롱아일랜드아이스티 , - , 임경호 , - , chaesang


// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class NLCM {
    public long nlcm(int[] num) {
        long answer = num[0],g;
    for(int i=1;i<num.length;i++){
      g=gcd(answer,num[i]);
            answer=g*(answer/g)*(num[i]/g);
    }
        return answer;
    }
    public long gcd(long a,long b){
    if(a>b)
      return (a%b==0)? b:gcd(b,a%b);
    else 
      return (b%a==0)? a:gcd(a,b%a);
  }
    public static void main(String[] args) {
        NLCM c = new NLCM();
        int[] ex = { 2, 6, 8, 14 };
        // 아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println(c.nlcm(ex));
    }
}
```

<br> 

위의 코드는 `유클리드 호제법`을 이용해 최대공약수로 최대공배수를 구하는 함수같은데 아직 재귀함수에 대해 완벽히 이해를 못한 상태라 정확한 리딩이 불가능하다. 다음에..다시 리딩을 도전해 봐야할 것 같다. 