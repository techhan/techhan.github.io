---
title: "[프로그래머스] 문자열 다루기 기본(JAVA)"
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

> 문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> s는 길이 1 이상, 길이 8 이하인 문자열입니다.
<br>

## 입출력 예

|s|answer|
|:------|:------|
|"a234"|false|
|"1234"|true|


<br>

## JAVA 풀이 과정

```java
class Solution {
    public boolean solution(String s) {
        boolean answer = true;
        if(s.length() == 4 || s.length() == 6){
            for(int i = 0; i < s.length(); i++){
                if(!(s.charAt(i) >= '0' && s.charAt(i) <= '9')){
                    answer = false;
                    break;
                }
            }
        }else{
            answer = false;
        }
        return answer;
    }
}
```

![결과](https://user-images.githubusercontent.com/70805241/115147459-05561c00-a096-11eb-9543-6c29a9fc7f3c.png)
{: width="600" height="600"}

<br>

음~ 쉽다. 이러면서 코드를 열심히 작성했는데 코드 실행으로 테스트 케이스는 가뿐하게 통과했으나 제출하니까 3 ~ 4개의 테스트 케이스 빼고는 모두 실패였다..! 그래서 문제를 계속 읽어봤는데 문자열의 길이가 `4 혹은 6`이고 이 부분을 놓쳐서 계속 실패가 뜬 거였다. 저 조건의 코드를 작성하고 제출하니까 통과되었다.



<br><br>




**다른 사람 풀이** <br>
```java
//  - , JegalJisu , 전은광 , - , - 외 60 명
class Solution {
  public boolean solution(String s) {
      if(s.length() == 4 || s.length() == 6){
          try{
              int x = Integer.parseInt(s);
              return true;
          } catch(NumberFormatException e){
              return false;
          }
      }
      else return false;
  }
}
```

<br>

다른 사람들은 `예외 처리`를 이용해 문제를 풀었다. 예외 처리를 많이 써봤지만 이렇게 알고리즘에서 사용하는 건 처음 봐서 엄청나게 놀라웠다. try 구문 안에 x라는 int 변수에 s 문자열을 int 자료형으로 변환하는 과정에서 숫자 외에 다른 문자가 들어가 있으면 catch 구문으로 넘어가 false를 반환하는 코드이다.

