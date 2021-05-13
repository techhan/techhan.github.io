---
title: "[프로그래머스] 폰켓몬(JAVA)"
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

> 당신은 폰켓몬을 잡기 위한 오랜 여행 끝에, 홍 박사님의 연구실에 도착했습니다. 홍 박사님은 당신에게 자신의 연구실에 있는 총 N 마리의 폰켓몬 중에서 N/2마리를 가져가도 좋다고 했습니다.<br>홍 박사님 연구실의 폰켓몬은 종류에 따라 번호를 붙여 구분합니다. 따라서 같은 종류의 폰켓몬은 같은 번호를 가지고 있습니다. 예를 들어 연구실에 총 4마리의 폰켓몬이 있고, 각 폰켓몬의 종류 번호가 [3번, 1번, 2번, 3번]이라면 이는 3번 폰켓몬 두 마리, 1번 폰켓몬 한 마리, 2번 폰켓몬 한 마리가 있음을 나타냅니다. 이때, 4마리의 폰켓몬 중 2마리를 고르는 방법은 다음과 같이 6가지가 있습니다. 
1. 첫 번째(3번), 두 번째(1번) 폰켓몬을 선택
2. 첫 번째(3번), 세 번째(2번) 폰켓몬을 선택
3. 첫 번째(3번), 네 번째(3번) 폰켓몬을 선택
4. 두 번째(1번), 세 번째(2번) 폰켓몬을 선택
5. 두 번째(1번), 네 번째(3번) 폰켓몬을 선택
6. 세 번째(2번), 네 번째(3번) 폰켓몬을 선택<br>

이때, 첫 번째(3번) 폰켓몬과 네 번째(3번) 폰켓몬을 선택하는 방법은 한 종류(3번 폰켓몬 두 마리)의 폰켓몬만 가질 수 있지만, 다른 방법들은 모두 두 종류의 폰켓몬을 가질 수 있습니다. 따라서 위 예시에서 가질 수 있는 폰켓몬 종류 수의 최댓값은 2가 됩니다.<br>
당신은 최대한 다양한 종류의 폰켓몬을 가지길 원하기 때문에, 최대한 많은 종류의 폰켓몬을 포함해서 N/2마리를 선택하려 합니다. N마리 폰켓몬의 종류 번호가 담긴 배열 nums가 매개변수로 주어질 때, N/2마리의 폰켓몬을 선택하는 방법 중, 가장 많은 종류의 폰켓몬을 선택하는 방법을 찾아, 그때의 폰켓몬 종류 번호의 개수를 return 하도록 solution 함수를 완성해주세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- nums는 폰켓몬의 종류 번호가 담긴 1차원 배열입니다.
- nums의 길이(N)는 1 이상 10,000 이하의 자연수이며, 항상 짝수로 주어집니다.
- 폰켓몬의 종류 번호는 1 이상 200,000 이하의 자연수로 나타냅니다.
- 가장 많은 종류의 폰켓몬을 선택하는 방법이 여러 가지인 경우에도, 선택할 수 있는 폰켓몬 종류 개수의 최댓값 하나만 return 하면 됩니다.


<br>

## 입출력 예

|nums|result|
|:------|:------|
|[3,1,2,3]|2|
|[3,3,3,2,2,4]|3|
|[3,3,3,2,2,2]|2|

<br>

## JAVA 풀이 과정

{% raw %}

```java
import java.util.*;
class Solution {
    public int solution(int[] nums) {
        Set<Integer> nSet = new HashSet<>();
        for(int i = 0; i < nums.length; i++){
            nSet.add(nums[i]);
        }
        
        if(nSet.size() > (nums.length / 2)) return nums.length / 2;

        return nSet.size();
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/118143789-aee6be00-b446-11eb-8bea-9d89f47015bc.png)



<br>

이번 문제도 지문이 길어 긴장했지만 천천히 생각해보니 그렇게 어려운 코드는 아니였다. 리턴 될 최댓값은 어쨌든 `N/2`를 넘지 않으면 되니 일단 중복을 제거해 종류의 수를 구하기 위해 `Set`을 사용했다. Set의 사이즈가 'N/2'보다 큰 경우에만 'N/2'를 리턴하도록 코드를 작성했다.

<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
//  김영수
import java.util.*;
class Solution {
    public int solution(int[] nums) {
        //1. 기존 length를 구한다.
        //2. 중복값을 제거한 length를 구한다.
        //3. 두 값중 최소값이 정답.
        List<Integer> list = new ArrayList<Integer>();
        for(int i = 0 ; i < nums.length; i++){
            if(!list.contains(nums[i])){
                list.add(nums[i]);
            }
        }

        return nums.length/2 > list.size()?list.size():nums.length/2;
    }
}
```

{% endraw %}

<br>

다른 코드는 `스트림`으로 풀이한 코드도 있었고 나와 똑같은 로직으로 푼 사람도 있었다. 위의 풀이는 'Set'이 아닌 `ArrayList`를 이용했고, `contains()` 메서드로 중복을 제거해 담았다.