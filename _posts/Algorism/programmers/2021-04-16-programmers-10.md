---
title: "[프로그래머스] 문자열 내 마음대로 정렬하기(JAVA)"
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

> 문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> strings는 길이 1 이상, 50이하인 배열입니다.<br>
strings의 원소는 소문자 알파벳으로 이루어져 있습니다.<br>
strings의 원소는 길이 1 이상, 100이하인 문자열입니다.<br>
모든 strings의 원소의 길이는 n보다 큽니다.<br>
인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.
<br>

## 입출력 예

|strings|n|return|
|:------|:------||:------|
|["sun", "bed", "car"]|1|["car", "bed", "sun"]|
|["abce", "abcd", "cdx"]|2|["abcd", "abce", "cdx"]|


<br>

## JAVA 풀이 과정 (답 찾아봄)

**초기 코드** <br>

```java
import java.util.ArrayList;
import java.util.Collections;
class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = new String[strings.length];
        ArrayList<String> list = new ArrayList<>();

        for(int i = 0; i < strings.length; i++){
            list.add(strings[i].substring(n));
        }
        
        Collections.sort(list);

        for(int i = 0; i < list.size(); i++){
            for(int j = 0; j < strings.length; j++){
                if(list.get(i).equals(strings[j].substring(n))){
                    answer[i] = strings[j];
                }
            }
        }
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/114868434-de4ae080-9e30-11eb-866d-ff1498acbc42.png)
{: width="600" height="600"}

<br>

이번 문제는 풀지 못했다. 일반 제일 처음에 작성한 코드가 저건데 저렇게만 해도 일단 코드 실행하면 두 번의 테스트 케이스 모두 `통과`로 나왔다. 근데 제출만 하면 세 개의 테스트 케이스 외에 모두 실패로 나왔다. 뭐가 문제일까 생각해봤다가 n번째 전의 문자열들도 정렬해 줄 필요성, 그리고 n번째 이후부터 중복되는 문자열이 분명히 있으니까 안쪽 for문 안에 if문에 진입 시 strings[j]의 값을 answer[i]에 저장하고, strings[j]의 공간을 null로 만들었다.


<br><br>

**두 번째 코드**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = new String[strings.length];
        ArrayList<String> list = new ArrayList<>();

        for(int i = 0; i < strings.length; i++){
            list.add(strings[i].substring(n));
        }
        
        Collections.sort(list);
        Arrays.sort(strings);
        
        for(int i = 0; i < list.size(); i++){
            for(int j = 0; j < strings.length; j++){
                if(strings[j] != null){
                    if(list.get(i).equals(strings[j].substring(n))){
                        answer[i] = strings[j];
                        strings[j] = null;
                        break;
                    }
                }
            }
        }
        return answer;
    }
}
```

<br><br>

n번째 이후 중복된 문자열을 위해 strings[j]에 null을 저장하는 코드와 break, 그리고 기존에 있던 if문 바깥쪽에 strings[j]가 null이 아니면 이라는 코드를 추가했고, strings 배열도 정렬 한 번 해줬다. 이렇게 완벽한 코드를 작성한 줄 알았으나.... <br>

![결과2](https://user-images.githubusercontent.com/70805241/115000528-ced5a100-9edd-11eb-9937-3aa352cecd24.png)

이 역시 3개의 테스트 케이스를 제외하고 모두 실패가 나왔다. ~~25점 그만줘요..~~ <br> 어디가 문제인지 해결해보려고 테스트 케이스를 여러 개 더 추가해서 돌려봤지만 모두 통과했다....! <br>
![테케](https://user-images.githubusercontent.com/70805241/115011397-8ae89900-9ee9-11eb-9d5c-c0a3af03b369.png)

<br> 어떻게 풀어야 하는 건지는 충분히 알겠으나, 내 생각을 코드로 녹여내는게 너무 어려웠다. 문자열 관련 메서드도 많이 모르기도 하고.... 그래서 어차피 잡고 있어도 못 풀 것 같아 시간 낭비하기 싫어, 답을 찾았다. <br>




**다른 사람 풀이** <br>
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.ArrayList;
class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = new String[strings.length];
        
        ArrayList<String> arr = new ArrayList<>();
        
        for(int i = 0; i < strings.length; i++){
            arr.add(strings[i].charAt(n) + strings[i]);
        }
        
        Collections.sort(arr);
        
        for(int i = 0; i < arr.size(); i++){
            answer[i] = arr.get(i).substring(1);
        }
        return answer;
    }
}
```

<br>

![결과3](https://user-images.githubusercontent.com/70805241/115013310-d308bb00-9eeb-11eb-8c5f-043a32894bcf.png)

드디어 통과되었다. 근데 뭔가 속도가 전체적으로 약간 느린 느낌이 든다. 테스트 1, 2, 5의 경우는 내 코드는 1.00ms 미만의 속도가 측정됐는데 위의 코드는 전체적으로 10.00ms가 넘는다;; 시간 관계상 내일 다시 분석해봐야할 것 같다.