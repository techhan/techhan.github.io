---
title: "[프로그래머스] 이상한 문자 만들기(JAVA)"
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

> 문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.<br>
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.
<br>

## 입출력 예

|s|return|
|:------|:------|
|"try hello world"|"TrY HeLlO WoRlD"|

<br>

## JAVA 풀이 과정

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        String[] word = s.split(" ", -1);

        for(int i = 0; i < word.length; i++){
            for(int j = 0; j < word[i].length(); j++){
                if(j % 2 == 0 || j == 0) answer += Character.toUpperCase(word[i].charAt(j));
                else answer += Character.toLowerCase(word[i].charAt(j));
            }
            if(i != word.length - 1) answer += " ";
        }
  return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/116017288-27453500-a67a-11eb-9329-2e47a97aa6e9.png)



<br>

쉽게 생각했었는데 생각보다 잘 안 풀리는 문제였다. `toUpperCase()`와 `toLowerCase()`를 사용했었는데 자꾸 에러가 떠서 구글링 해봤더니 문자열인 String 타입이랑 char 타입이 사용하는 법이 좀 달라 자꾸 에러가 발생하는 거였다. 위의 메서드의 문법까지 지켜서 코드 실행하니 테스트 케이스 통과라 제출을 눌렀더니 실패가 좌르륵 출력되었다. 디버깅을 하는데 도저히 어느 부분에서 틀린지 모르겠어서 테스트 케이스를 추가해봤다. <br>
![테스트케이스](https://user-images.githubusercontent.com/70805241/116090391-c56ae680-a6de-11eb-9bcb-c0c9d9d4b785.png) <br>

위의 테스트 케이스도 모두 통과되어서 결국 문제점을 찾지 못하고 '질문하기' 버튼을 눌렀다. 이것저것 찾아보니 문제의 원인은 바로 `각 단어는 하나 이상의 공백문자로 구분되어 있습니다.` 
이 부분이었다. 공백이 두 개가 들어올 수도 있고, 세 개가 들어올 수도 있는 부분을 아예 생각을 못 했다. `split` 메서드에 인자에 `-1`을 추가하니 통과되었다. 

<br><br>


**다른 사람 풀이** <br>

```java
// Sunhee Shin , - , 정선욱 , 이상호 , - 외 43 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.

class Solution {
  public String solution(String s) {

        String answer = "";
        int cnt = 0;
        String[] array = s.split("");

        for(String ss : array) {
            cnt = ss.contains(" ") ? 0 : cnt + 1;
            answer += cnt%2 == 0 ? ss.toLowerCase() : ss.toUpperCase(); 
        }
      return answer;
  }
}
```

<br>

위의 코드는 `삼항연산자`로 count 부분과 짝수, 홀수를 구해서 문제를 풀이했다. 코드가 엄청나게 짧아졌고, 간결해졌다.


<br>

```java
//Sanggi Son , Soongvely , 구슬기 , YNNJN
class Solution {
  public String solution(String s) {
        char[] chars = s.toCharArray();
        int idx = 0;

        for (int i = 0; i < chars.length; i++) {
            if (chars[i] == ' ')
                idx = 0;
            else
                chars[i] = (idx++ % 2 == 0 ? Character.toUpperCase(chars[i]) : Character.toLowerCase(chars[i]));
        }

        return String.valueOf(chars);
  }
}
```

<br>

개인적으로는 위의 코드가 더 알아보기 쉽고, 더 깔끔한 것 같다.