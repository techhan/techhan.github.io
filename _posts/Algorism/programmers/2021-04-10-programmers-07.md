---
title: "[프로그래머스] 체육복(JAVA)"
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

> 점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.<br><br>
전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 전체 학생의 수는 2명 이상 30명 이하입니다.<br>
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.<br>
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.<br>
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.<br>
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.
<br>

## 입출력 예

|n|lost|reserve|return
|:------|:------||:------|:------|
|5|[2, 4]|[1, 3, 5]|5|
|5|[2, 4]|[3]|4|
|3|[3]|[1]|2|

<br>

## JAVA 풀이

```java
import java.util.*;

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        n -= lost.length;
        Arrays.sort(lost);
        Arrays.sort(reserve);

        for(int i = 0; i < reserve.length; i++){
            for(int j = 0; j < lost.length; j++){
                if(reserve[i] == lost[j]){
                    reserve[i] = -1;
                    lost[j] = -1;
                    n++;
                }
            }
        }

        for(int i = 0; i < reserve.length; i++){
            for(int j = 0; j < lost.length; j++){
                if(lost[j] > 0) {
                    if(lost[j] -1 == reserve[i] || lost[j] +1 == reserve[i]){
                    n++;
                    lost[j] = 0;
                    reserve[i] = 0;
                     }
                }
            }
        }
        return n;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114272912-f72f4c80-9a52-11eb-9589-a673d5034de7.png)
{: width="600" height="600"}

<br>

맨 처음에 제출했을 때 12개의 테스트 케이스 중에서 3개만 통과하고 나머지는 모두 실패가 떴었다. 생각해보니 입력 된 테스트 케이스 중에서 정렬되지 않은 순서로 들어오는 값들도 있을 것 같아 `Arrays.sort()`를 추가해줬더니 그래도 반 이상이 통과되었다. 다시 한 번 코드를 잘 살펴보니 첫 번째 이중 for문에 n++만 체크해줬지 해당 배열의 값에 변화를 주지 않아 두 번째 이중 for문에서 중복 체크가 되는 문제가 발생한 걸 깨닫고 위의 코드처럼 수정하니 모두 통과할 수 있었다!


<br>


```java
// - , - , 한만혁 , 백대현 , 권도형 외 13 명
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int[] people = new int[n];
        int answer = n;

        for (int l : lost) 
            people[l-1]--;
        for (int r : reserve) 
            people[r-1]++;

        for (int i = 0; i < people.length; i++) {
            if(people[i] == -1) {
                if(i-1>=0 && people[i-1] == 1) {
                    people[i]++;
                    people[i-1]--;
                }else if(i+1< people.length && people[i+1] == 1) {
                    people[i]++;
                    people[i+1]--;
                }else 
                    answer--;
            }
        }
        return answer;
    }
}
```

위의 코드는 깔끔하긴 한데 솔직히 말하자면 한눈에 딱 들어오진 않는 것 같다. 코드가 잘못 작성된 게 아니라 내 실력이 그만큼 얕다는 걸 느낄 수 있었다. 이 짧은 코드도 한눈에 못 알아보다니… 너무 내가 생각하는 코드 위주로 해석을 하려는 것 같다. <br>

또 `HashSet`을 이용해서 코드를 작성하신 분들도 있었다.

```java
//박수민 , 서순호 , -
import java.util.HashSet;
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer=n-lost.length;
        HashSet<Integer> ko = new HashSet<Integer>();
        for(int k : reserve) {
            ko.add(k);
        }
        for(int i =0;i<lost.length;i++) {
            if(ko.contains(lost[i])) {
                //System.out.println("내껀내가입지");
                answer++;
                ko.remove(lost[i]);
                lost[i]=-1;
            }
        }


        for(int i =0;i<lost.length;i++) {
            //System.out.println(i);

            if(ko.contains(lost[i]-1)) {
                //System.out.println("있다");
                answer++;
                ko.remove(lost[i]-1);
            }else if(ko.contains(lost[i]+1)) {
                //System.out.println("있다");
                answer++;
                ko.remove(lost[i]+1);
            }
            //System.out.println("없다");
        }


        return answer;
    }
}
```