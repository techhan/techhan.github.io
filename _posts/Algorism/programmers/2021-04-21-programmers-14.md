---
title: "[프로그래머스] 문자열 내림차순으로 배치하기(JAVA)"
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

> 문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> str은 길이 1 이상인 문자열입니다.
<br>

## 입출력 예

|s|return|
|:------|:------|
|"Zbcdefg"|"gfedcbZ"|

<br>

## JAVA 풀이 과정

```java
import java.util.Arrays;

class Solution {
    public String solution(String s) {
        char[] cArr = new char[s.length()];
        for(int i = 0; i < s.length(); i++){
            cArr[i] = s.charAt(i);
        }
        
        Arrays.sort(cArr);
        StringBuilder answer = new StringBuilder(new String(cArr));
        
        return answer.reverse().toString();
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/115523621-387ff180-a2c8-11eb-9645-cc96b5cfe138.png)



<br>

처음에는 아스키코드 값을 비교해서 삽입 정렬로 정렬할까 했는데 코드가 길어질 것 같아 `Arrays.sort`로 생각을 바꿨다. 먼저 char 배열을 String s의 길이만큼 선언하고, for문을 돌려 char 배열에 문자열 한 글자씩을 대입했다. 그리고 char 배열 정렬 후에 생각 없이 String answer를 사용했었는데 이 [포스팅](https://techhan.github.io/study/interview-02/)에서 정리했던 게 생각나서 `StringBuilder`로 answer를 선언 후, 문자열을 저장했다. 그리고 정렬되어 있는 answer를 내림차순으로 출력하기 위해 `.reverse()`를 사용했고, `.toString`을 붙여주었다.



<br><br>

**다른 사람 풀이** <br>

```java
//- , - , - , - , - 외 108 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
import java.util.Arrays;

public class ReverseStr {
    public String reverseStr(String str){
    char[] sol = str.toCharArray();
    Arrays.sort(sol);
    return new StringBuilder(new String(sol)).reverse().toString();
    }

    // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String[] args) {
        ReverseStr rs = new ReverseStr();
        System.out.println( rs.reverseStr("Zbcdefg") );
    }
}

```

<br>

이 코드는 내 로직과 똑같은데 다만 더 짧을 뿐이다. 나는 for문으로 char 배열에 하나씩 담은 반면, 이 코드에서는 `toCharArray()` 메서드를 사용해 문자열을 char 배열에 담았다. 그리고 정렬 후, answer를 따로 선언하지 않고 바로 return 부분에 StringBuilder를 사용했다.