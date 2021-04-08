---
title: "[프로그래머스] 2016년(JAVA)"
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

> 2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 `SUN,MON,TUE,WED,THU,FRI,SAT`입니다. <br> 예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 "TUE"를 반환하세요.

<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> 2016년은 윤년입니다.<br>
2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)



<br>

## 입출력 예


|a|b|return|
|:---------|:------|:------|
|5|24|"TUE"|


<br>

## JAVA 풀이

```java
import java.util.Calendar;

class Solution {
    public String solution(int a, int b) {
        String answer = "";
        
        String[] week = {"SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"};
        Calendar cal = Calendar.getInstance();
        cal.set(Calendar.YEAR, 2016); 
        cal.set(Calendar.MONTH, a - 1);
        cal.set(Calendar.DAY_OF_MONTH, b);
        answer = week[cal.get(Calendar.DAY_OF_WEEK) - 1];

        return answer;
    }
}
```


![결과](https://user-images.githubusercontent.com/70805241/113995299-141c2200-9891-11eb-9356-4e972e512cb9.png)

<br>

요일 구하는 문제는 예전에 한 번 풀어봐서 `Calendar` 클래스를 기억해 낼 수 있었다. 다른 사람들의 풀이를 보니 배열로 푼 사람들도 있었고, 똑같이 Calendar 클래스로 푼 사람들도 있었다. 제일 기억에 남는 코드가 두 개 있었다.

```java
//덱스또님의 코드
import java.util.*;

class TryHelloWorld
{
    public String getDayName(int month, int day)
    {
        Calendar cal = new Calendar.Builder().setCalendarType("iso8601")
                // Calenda 객체를 빌더 패턴을 이용해 생성
                        .setDate(2016, month - 1, day).build();
                         // 날짜 매개변수(year, month, dayOfMonth)로 setter를 이용해 값을 넣는다. 
        return cal.getDisplayName(Calendar.DAY_OF_WEEK, Calendar.SHORT, new Locale("ko-KR")).toUpperCase();
        // getDisplayName ( int  field,  int  style, Locale locale)
        // field : 년월일 전달
        // style : 매개 변수로 전달 된 필드의 문자열 표현에 적용할 스타일
        // locale : 문자열 표현
        // toUpperCase : 모든 영문자를 대문자로

    }
    public static void main(String[] args)
    {
        TryHelloWorld test = new TryHelloWorld();
        int a=5, b=24;
        System.out.println(test.getDayName(a,b));
    }
}


-----------------------------------------------------------
// 김지예님 , 이용준님 , 이상근님 외 10 명 코드
class TryHelloWorld
{
    public String getDayName(int a, int b) {
        String answer = "";
        String[] day = { "FRI", "SAT", "SUN", "MON", "TUE", "WED", "THU" };
        int[] date = { 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
        int allDate = 0;
        for (int i = 0; i < a - 1; i++) {
            allDate += date[i];
        }
        allDate += (b - 1);
        answer = day[allDate % 7];

        return answer;
    }
    public static void main(String[] args)
    {
        TryHelloWorld test = new TryHelloWorld();
        int a=5, b=24;
        System.out.println(test.getDayName(a,b));
    }
}
```

첫 번째 코드의 경우는 처음 보는 메서드가 너무 많아서 해석하는 데 오래 걸렸다. 두 번째 코드는 배열을 사용한 코드인데 요일을 담은 day 배열, 일 수를 담은 date라는 배열을 생성해 for문을 돌리고 a - 1 값만큼 allDate에 저장, 그리고 allDate에 b - 1 값을 저장해 % 7을 한 값을 인덱스로 사용해 day 배열 안에 있는 값을 return 했다. 내 기준 제일 깔끔하고 보기 좋았던 코드라 가져왔다.


### 참고

- [javatpoint](https://www.javatpoint.com/post/java-calendar-getdisplayname-method)
- [abss.tistory](https://abss.tistory.com/68)