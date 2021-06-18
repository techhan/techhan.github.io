---
title: "[프로그래머스] 소수 찾기(JAVA)"
excerpt: "Level 2"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_2
---


> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.<br>

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.<br>
<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.


<br>
<br>


> ## 입출력 예

|numbers|return|
|:------|:------|
|"17"|3|
|"011"|2|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.*;
class Solution {
  ArrayList<Integer> result;
    boolean[] visited;
    
    public int solution(String numbers) {
        result = new ArrayList<Integer>();
        visited = new boolean[numbers.length()];
        int[] nums = new int[numbers.length()];
        
        for(int i = 0; i < nums.length; i++) {
            nums[i] = Integer.parseInt(numbers.charAt(i)+"");
        }
        
        //자리 수 마다 해당 배열을 perm 메서드에 보낸다.
        for(int i = 1; i <= numbers.length(); i++) {
            int[] resultArr = new int[i];
            perm(nums, resultArr, nums.length, i, 0);
        }
        
        return result.size();
        
    }
    public boolean isPrime(int num) {
        if(num <= 1) {
            return false;
        }
        if(num == 2 || num == 3) {
            return true;
        }
        
        int end = (int) Math.sqrt(num);
        for(int i = 2; i <= end; i++) {
            if(num % i == 0) {
                return false;
            }
        }
        return true;
    }
    
    
    public void perm(int[] nums, int[] resultArr, int n, int r, int index) {
        if(index == r) {
            String realNum = "";
            for(int i = 0; i < resultArr.length; i++) {
                realNum += resultArr[i];
            }
            
            int num = Integer.parseInt(realNum);
            if(isPrime(num)) {
                if(!result.contains(num)) {
                    result.add(num);
                }
            }
            return;
        }
        
        for(int i = 0; i < nums.length; i++) {
            if(!visited[i]) {
                visited[i] = true;
                resultArr[index] = nums[i];
                perm(nums, resultArr, n, r, index+1);
                resultArr[index] = 0;
                visited[i] = false;
            }
        }
    }

}
```

{% endraw %}


![결과](https://user-images.githubusercontent.com/70805241/122519566-907b7000-d04d-11eb-903a-3a7fbb75eab5.png)
 <br>


결론을 먼저 말하자면 순열을 구하는 부분을 도저히 모르겠어서 답을 봤다. <br>
일단 생각은 완벽했다.
1. numbers로 만들 수 있는 가장 큰 수 구하기
2. 에라토스테네스의 체로 가장 큰 수 까지의 소수를 모두 구하기
3. numbers 순열을 구해서 소수 배열에 있는 수면 answer++하기

2번 까지는 무난하게 구현했으나 3번 순열이 문제였다. 순열을 한 번도 구해 본 적이 없어서 못해서 하루를,,, 씨름하다가 답을 보고 제출했다. 그리고 코드를 잘못 짠 걸수도 있으나,, 큰 수 까지의 소수를 모두 구하는 과정이 너무 오래 걸리는 건지 코드 실행이 되지 않았다 ㅎㅎ 그래서 그냥 어떤 수마다 소수인지 아닌지 판별하는 방식으로 변경했다.

<br><br>

**다른 사람의 풀이** <br>

```java
// 정인섭 , 테스트 , - , Tim J. Lee , 김여천 외 10 명
import java.util.HashSet;
class Solution {
    public int solution(String numbers) {
        HashSet<Integer> set = new HashSet<>();
        permutation("", numbers, set);
        int count = 0;
        while(set.iterator().hasNext()){
            int a = set.iterator().next();
            set.remove(a);
            if(a==2) count++;
            if(a%2!=0 && isPrime(a)){
                count++;
            }
        }        
        return count;
    }

    public boolean isPrime(int n){
        if(n==0 || n==1) return false;
        for(int i=3; i<=(int)Math.sqrt(n); i+=2){
            if(n%i==0) return false;
        }
        return true;
    }

        public void permutation(String prefix, String str, HashSet<Integer> set) {
        int n = str.length();
        //if (n == 0) System.out.println(prefix);
        if(!prefix.equals("")) set.add(Integer.valueOf(prefix));
        for (int i = 0; i < n; i++)
          permutation(prefix + str.charAt(i), str.substring(0, i) + str.substring(i+1, n), set);

    }

}
```

순열 부분이 좀 더 짧은 코드!
