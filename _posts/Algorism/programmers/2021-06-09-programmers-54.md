---
title: "[프로그래머스] 위장(JAVA)"
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

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다. <br>
예를들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다. <br>

![설명](https://blog.kakaocdn.net/dn/A3vn3/btq6QOHzT40/A4xsdKXEsFJZ1h7iyKgLc0/img.png)

<br>
스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_'로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.


<br>
<br>


> ## 입출력 예

|clothes|return|
|:------|:------|
|[["yellowhat", "headgear"], ["bluesunglasses", "eyewear"], ["green_turban", "headgear"]]|5|
|[["crowmask", "face"], ["bluesunglasses", "face"], ["smoky_makeup", "face"]]|3|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.HashMap;
import java.util.Iterator;
class Solution {
    public int solution(String[][] clothes) {
        int answer = 1;
        HashMap<String, Integer> map = new HashMap<>();
        for(int i = 0; i < clothes.length; i++){
            if(!map.containsKey(clothes[i][1])){
                map.put(clothes[i][1], 1);
            } else {
                map.put(clothes[i][1], map.get(clothes[i][1]) + 1);
            }
        }
        
        Iterator<Integer> it = map.values().iterator();
        while(it.hasNext()){
            answer *= it.next().intValue() + 1;
        }
        return answer-1;
    }
}
```

{% endraw %}

![결과](https://blog.kakaocdn.net/dn/cgIcbD/btq6VEpGAQh/xyUkoSEgxHWXYzflxljNF1/img.png)


<br>

이번 문제는 HashMap과 Iterator를 사용해서 풀이했다. 오랜만에 Map을 사용해보니 참으로 어색하다. 
Map을 잘 사용해보지 않은 편이라 함수 몇 개는 구글링을 이용했다. 

`containsKey(Key)` 함수는 Map에 키가 있는지 확인하는 함수로 키가 있으면 true, 없으면 false를 반환한다.
이와 비슷한 `containsValue(value)` 함수는 값이 있으면 true, 없으면 false를 반환한다.

<br><br>

