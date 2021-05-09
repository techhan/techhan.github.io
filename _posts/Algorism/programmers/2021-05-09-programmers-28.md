---
title: "[프로그래머스] 하샤드 수(JAVA)"
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

> 양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. <br> 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> x는 1 이상, 10000 이하인 정수입니다.
<br>

## 입출력 예

|arr|return|
|:------|:------|
|10|true|
|12|true|
|11|false|
|13|false|


<br>

## JAVA 풀이 과정

```java
class Solution {
    public boolean solution(int x) {
        boolean answer = true;
        String xStr = x + "";
        int sum = 0;
        for(int i = 0; i < xStr.length(); i++){
            sum += xStr.charAt(i) - '0';
        }
        
        if(x % sum != 0) return false;
        return answer;
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/117560931-3510a680-b0cd-11eb-993f-6741d5f3dec8.png)


<br>

먼저 매개 변수 x를 String 타입 변수인 xStr를 선언해 x를 문자열로 만들어 xStr에 대입했다. 그리고 xStr의 길이만큼 for문을 돌려 sum 변수에 자릿수를 하나씩 누적 저장했다. 그리고 x가 sum으로 나누어 떨어지지 않으면 false를 리턴하게 코드를 작성했다.

<br><br>


**다른 사람 풀이** <br>

```java
// - , - , 조조조 , - , -
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class HarshadNumber{
    public boolean isHarshad(int num){

    String[] temp = String.valueOf(num).split("");

    int sum = 0;
    for (String s : temp) {
        sum += Integer.parseInt(s);
    }

    if (num % sum == 0) {
            return true;
    } else {
      return false;
    }
    }

       // 아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void  main(String[] args){
        HarshadNumber sn = new HarshadNumber();
        System.out.println(sn.isHarshad(18));
    }
}
```

<br>

위의 코드는 num을 String 타입으로 만들고, `split()`을 사용해 String 배열에 한 자리씩 잘라서 대입했다. 그리고 향상된 for문으로 temp 배열에 있는 값을 하나씩 꺼내서 `Integer.parseInt()`를 사용해 String 타입을 Int 타입으로 변환해 연산했다. 그나저나 이제 야매로 배운 '숫자 + ""' 이런식으로 String 타입으로 바꾸지 말고 `String.valueOf()`를 사용해서 바꾸는 연습을 해야할 것 같다.