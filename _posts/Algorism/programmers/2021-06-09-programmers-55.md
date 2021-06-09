---
title: "[프로그래머스] 기능개발(JAVA)"
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

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.<br>

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.<br>

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.


<br>
<br>


> ## 입출력 예

|progresses|speeds|return|
|:------|:------|:------|
|[93, 30, 55]|[1, 30, 5]|[2, 1]|
|[95, 90, 99, 99, 80, 99]|[1, 1, 1, 1, 1, 1]|[1, 3, 2]|



<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int[] temp = new int[100];
        int day = -1;
        for(int i = 0; i < progresses.length; i++){
            while(progresses[i] + (speeds[i] * day) < 100){
                day++;
            }
            temp[day]++;
        }
        int cnt = 0;
        
        for(int n : temp){
            if(n != 0) cnt++;
        }
        
        int[] answer = new int[cnt];
        
        cnt = 0;
        for(int n : temp){
            if(n != 0) answer[cnt++] = n;
        }
        return answer;
    }
}
```

{% endraw %}


![결과](https://blog.kakaocdn.net/dn/AFpJE/btq6YmhE2mE/3dcuKrKjo84GMSPfJOACjK/img.png)


<br>

스택이나 큐로 멋지게 풀어보고 싶었지만 능력 부족으로 인해 헤매다가 결국 배열로 풀이했다. 그렇다고 내가 작성한 코드가 좋은 코드도 아닌 것 같다. 더 열심히 공부해야 함을 매우매우매우 느껴버린 오늘의 문제....

<br><br>

**다른 사람의 풀이** <br>

```java
// 김기준 , - , 임재성 , - , - 외 38 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.ArrayList;
import java.util.Arrays;
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int[] dayOfend = new int[100];
        int day = -1;
        for(int i=0; i<progresses.length; i++) {
            while(progresses[i] + (day*speeds[i]) < 100) {
                day++;
            }
            dayOfend[day]++;
        }
        return Arrays.stream(dayOfend).filter(i -> i!=0).toArray();
    }
}
```

위의 코드는 람다식으로 풀이했다고 한다. 람다식을 배워 본 적이 없어 맨 밑의 return 부분을... 정확히 이해는 못하겠으나 dayOfend 배열 중 0이 아닌 것들만 배열로 반환하는 것 같다. <br><br>

**큐를 이용한 풀이** <br>


```java
// HamYoungChan , - , - , 최건우 , 민경재 외 1 명

// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        Queue<Integer> q = new LinkedList<>();
        List<Integer> answerList = new ArrayList<>();

        for (int i = 0; i < speeds.length; i++) {
            double remain = (100 - progresses[i]) / (double) speeds[i];
            int date = (int) Math.ceil(remain);

            if (!q.isEmpty() && q.peek() < date) {
                answerList.add(q.size());
                q.clear();
            }

            q.offer(date);
        }

        answerList.add(q.size());

        int[] answer = new int[answerList.size()];

        for (int i = 0; i < answer.length; i++) {
            answer[i] = answerList.get(i);
        }

        return answer;
    }
}
```

