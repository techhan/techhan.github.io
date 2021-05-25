---
title: "[프로그래머스] 소수 만들기(JAVA)"
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

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

<br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

<br>

> ## 입출력 예

|nums|result|
|:------|:------|
|[1,2,3,4]|1|
|[1,2,7,6,4]|4|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int isPrime(int num){
        boolean flag = true;
        if(num <= 7) return 1;
        for(int i = 3; i < num; i+=2){
            if(num % i == 0) flag = false;
        }
        
        if(flag) return 1;
        return 0;
    }
    
    public int solution(int[] nums) {
        int answer = 0;
        int sum = 0;
        for(int i = 0; i < nums.length-2; i++){
            for(int j = i + 1; j < nums.length - 1; j++){
                for(int k = j + 1; k < nums.length; k++){
                    sum = nums[i] + nums[j] + nums[k];
                    if(sum % 2 != 0) answer += isPrime(sum);
                }
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>


![결과](https://user-images.githubusercontent.com/70805241/119529226-ddf11e00-bdbc-11eb-82f9-9db73b2b28c6.png)



<br>

어떠한 규칙이 있을까 고민 좀.. 해보다가 모르겠어서 무려 3개의 중첩 for문을 사용했다. 배열 안에 있는 값들을 3개씩 더하는거니 for문을 세 개 썼고, 제일 안 쪽 for문에서 세 개의 값을 모두 더해 만약 sum의 값이 짝수가 아니면 isPrime() 함수를 호출했다. <br>

isPrime() 함수에서는 sum 값을 매개 변수로 받아와 num에 저장했으며, num이 만약 7 이하의 숫자면 1을 바로 반환했고, 9 이상의 숫자면 for문을 돌려 소수인지 아닌지 판별했다. 


<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
//  - , Jeong SuCheol
import java.util.Arrays;

class Solution {
    public int solution(int[] nums) {
        int ans = 0;

        for(int i = 0; i < nums.length - 2; i ++){
            for(int j = i + 1; j < nums.length - 1; j ++){
                for(int k = j + 1; k < nums.length; k ++ ){
                    if(isPrime(nums[i] + nums[j] + nums[k])){
                        ans += 1;  
                    } 
                }
            }
        }
        return ans;
    }
    public Boolean isPrime(int num){
        int cnt = 0;
        for(int i = 1; i <= (int)Math.sqrt(num); i ++){
            if(num % i == 0) cnt += 1; 
        }
        return cnt == 1;
    }
}
```

{% endraw %}

<br>

위의 코드는 for문은 똑같이 구성했고, 제일 안쪽 for문에서 isPrime()을 바로 호출했다. isPrime() 메서드는 return 값이 Boolean으로 작성되었는데 내가 Boolean 리턴 타입을 많이 사용해본 적이 없어서 약간 신기했다. 1 이상은 true, 0은 false라는 점을 이용한 것 같다. 그리고 Math.sqrt() 메서드를 for문에 사용했다. 알고 있으면서 평소에 잘 안 쓰는 메서드는 참 기억해 내기 어렵다.