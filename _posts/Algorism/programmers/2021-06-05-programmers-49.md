---
title: "[프로그래머스] 최댓값과 최솟값(JAVA)"
excerpt: "Level 2"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_1
---


> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 "(최소값) (최대값)"형태의 문자열을 반환하는 함수, solution을 완성하세요.<br>
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.
<br>
<br>


> ## 입출력 예

|s|answer|
|:------|:------|
|"1 2 3 4"|"1 4"|
|"-1 -2 -3 -4"|"-4 -1"|
|"-1 -1"|"-1 -1"|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.Arrays;
class Solution {
    public String solution(String s) {
        String[] numStr = s.split(" ");
        int[] nums = new int[numStr.length];
        for(int i = 0; i < nums.length; i++){
            nums[i] = Integer.parseInt(numStr[i]);
        }
        
        Arrays.sort(nums);
        
        return nums[0] + " " + nums[nums.length-1];
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/120901205-5fc23080-c674-11eb-8d41-279feb3aac2b.png)
 <br>



<br><br>


<br><br>


**다른 사람의 풀이** <br>

```java
// - , - , - , - , - 외 49 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class GetMinMaxString {
    public String getMinMaxString(String str) {
        String[] tmp = str.split(" ");
        int min, max, n;
        min = max = Integer.parseInt(tmp[0]);
        for (int i = 1; i < tmp.length; i++) {
                n = Integer.parseInt(tmp[i]);
            if(min > n) min = n;
            if(max < n) max = n;
        }

        return min + " " + max;

    }

    public static void main(String[] args) {
        String str = "1 2 3 4";
        GetMinMaxString minMax = new GetMinMaxString();
        //아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println("최대값과 최소값은?" + minMax.getMinMaxString(str));
    }
}
```

<br> 

사실 제일 처음엔 위의 방법으로 풀이했다. 그런데 전체적으로 속도가 느리게 나와서 위의 코드로 변경했다. 근데 똑같이 느림 ㅎㅎ <br>

