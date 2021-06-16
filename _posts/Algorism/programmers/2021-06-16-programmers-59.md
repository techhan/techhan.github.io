---
title: "[프로그래머스] 가장 큰 수(JAVA)"
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

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.<br>

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.<br>

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.<br>
<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.


<br>
<br>


> ## 입출력 예

|numbers|return|
|:------|:------|
|[6, 10, 2]|"6210"|
|[3, 30, 34, 5, 9]|"9534330"|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
// 틀린코드

import java.util.Arrays;
class Solution {
    public String solution(int[] numbers) {
        StringBuffer answer = new StringBuffer();
        
        String[] numStr = new String[numbers.length];
        for(int i = 0; i < numbers.length; i++){
            numStr[i] = String.valueOf(numbers[i]);
        }
        
        boolean flag = true;
        for(String s : numStr){
            if(!s.equals("0")) flag = false;
        }
        if(flag) return "0";
        
        
        Arrays.sort(numStr);

        for(int i = 1; i < numStr.length; i++){
            if(numStr[i].length() >= 2){
                if(numStr[i].charAt(0) == numStr[i-1].charAt(0))
                {   
                    String max = numStr[i] + numStr[i-1];
                    String max2 = numStr[i-1] + numStr[i];
                    if(Integer.parseInt(max) < Integer.parseInt(max2)) {
                        String temp = numStr[i-1];
                        numStr[i-1] = numStr[i];
                        numStr[i] = temp;
                    }
                    
                 }
            }
                
        }
        
        for(int i = numStr.length-1; i >= 0; i--){
            answer.append(numStr[i]);
        }
        
        return answer.toString();
    }
}
```

{% endraw %}


![결과](https://user-images.githubusercontent.com/70805241/122193424-6f8d1080-cecf-11eb-8bff-6da95943b80a.png)
 <br>

프로그래머스에서 기본적으로 제공해주는 테스트케이스를 모두 통과했는데 제출하면 저렇게 테스트 케이스 1~6이 실패로 뜬다. 그래도 맨 처음 제출했을 땐 고작 하나만 통과해서 9.1이란 웃긴 점수를 받았는데 몇 개씩 고치다보니 7~11까지는 통과가 되었다..^^ 시간상 답을 봤다. <br><br>

```java
// 정답코드
import java.util.*;
class Solution {
    public String solution(int[] numbers) {
        StringBuffer answer = new StringBuffer();
        
        String[] str =new String[numbers.length];
        
        for(int i = 0; i < numbers.length; i++){
            str[i] = String.valueOf(numbers[i]);
        }
        
        // 내림차순 정렬
        Arrays.sort(str, new Comparator<String>(){
            @Override
            public int compare(String a, String b){
                return (b+a).compareTo(a+b);
            }
        });
        
        if(str[0].equals("0")) return "0";
        
        for(String s : str) answer.append(s);
        
        return answer.toString();
    }
}
```

<br>

CompareTo() 함수는 저번에 한 번 정리했었는데 그 이후로 사용해본 적이 없어 이번에 활용하지 못했다. 역시 여러 번 써봐야 손에 익는 것 같다. a.compareTo(b)는 앞에서부터 비교하다가 다른 문자열이 나오면 'a-b' 순서로 해당 문자의 아스키코드 값을 뺀 결과(int)를 리턴한다. 위 메소드에서 a, b 순서로 있을 때 (b+a).compareTo(a+b)를 했을 경우 'b+a'가 더 크면 자리를 바꿔준다. <br>


<br><br>

**다른 사람의 풀이** <br>

```java
// 김형민 , - , - , 승환 , - 외 11 명
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Solution {
    public String solution(int[] numbers) {
        String answer = "";

        List<Integer> list = new ArrayList<>();
        for(int i = 0; i < numbers.length; i++) {
            list.add(numbers[i]);
        }
        Collections.sort(list, (a, b) -> {
            String as = String.valueOf(a), bs = String.valueOf(b);
            return -Integer.compare(Integer.parseInt(as + bs), Integer.parseInt(bs + as));
        });
        StringBuilder sb = new StringBuilder();
        for(Integer i : list) {
            sb.append(i);
        }
        answer = sb.toString();
        if(answer.charAt(0) == '0') {
            return "0";
        }else {
            return answer;
        }
    }
}
```

Arrays.sort() 대신 Collections.sort()를 사용하였으며 람다식을 사용한 코드이다. 