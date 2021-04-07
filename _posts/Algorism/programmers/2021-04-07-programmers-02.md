---
title: "[프로그래머스] 완주하지 못한 선수(JAVA)"
excerpt: "Level 1"
categories: 
  - Algorithm
tags: 
  - Programmers
  - Java
  - Level_1
---



## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

> 수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다. <br> 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다. <br>
completion의 길이는 participant의 길이보다 1 작습니다. <br>
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다. <br>
참가자 중에는 동명이인이 있을 수 있습니다. 

<br>

## 입출력 예


|participant|completion|return|
|:---------|:------|:------|
|["leo", "kiki", "eden"]|["eden", "kiki"]|"leo"|
|["marina", "josipa", "nikola", "vinko", "filipa"]|["josipa", "filipa", "marina", "nikola"]|"vinko"|
|["mislav", "stanko", "mislav", "ana"]|["stanko", "ana", "mislav"]|"mislav"|

<br>

## JAVA 풀이

```java
import java.util.Arrays;

class Solution {
    public String solution(String[] participant, String[] completion) {
        Arrays.sort(participant);
        Arrays.sort(completion);
        
        int i;
        for(i = 0; i < completion.length; i++){
            if(!participant[i].equals(completion[i])){
                return participant[i];
            }
        }
        return participant[i];
    }
}
```


![완주하지못한선수](https://user-images.githubusercontent.com/70805241/113862328-37889380-97e3-11eb-9342-4a667ee53059.png)

<br>

배열 길이의 추가 삭제가 필요한 것 같지 않아 굳이 ArrayList를 쓰지 않아도 된다고 판단했다. 그래서 이중 for문으로 participant와 completion 돌려서 두 개의 배열을 비교해 없으면 리턴하는 코드를 짰더니 테스트 3번을 통과하지 못했다.<br>
![테스트3](https://user-images.githubusercontent.com/70805241/113864827-52a8d280-97e6-11eb-8fa8-e239f70f4f07.png) <br>
이게 뭐야! 하면서 테스트 케이스를 자세히 보니 `동명이인`의 경우를 생각하지 못했던 걸 깨달았다. 동명이인의 경우를 어떻게 처리해야 할까 여러 방법을 고민했다.
1. flag 사용 --> 먼저 participant 배열을 한 번 돌려 동명이인을 찾아내고 이중 for문을 돌릴 때 사용할까 했는데 이 경우 동명이인이 두 명일 때만 가능했다.
2. 동명이인을 담는 배열 생성 --> 동명이인들을 모두 담아서 인덱스를 카운트로 사용해 이중 for문을 돌릴 때마다 cnt-1이 되도록 하고 cnt가 0이 아닐 때 그 동명이인을 리턴하도록 만들려 했는데 너무 비효율적인 것 같았다.
<br>

이 두 방법 외에 더 생각해 봤는데 `Arrays.sort()`가 생각나서 차라리 두 배열을 모두 정렬시키고 나서 값을 비교하면 굳이 이중 for문을 사용하지 않아도 될 것 같아서 위의 코드를 완성했다. 