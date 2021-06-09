---
title: "[프로그래머스] 전화번호 목록(JAVA)"
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

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.


- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.
- 같은 전화번호가 중복해서 들어있지 않습니다.


<br>
<br>


> ## 입출력 예

|phone_book|return|
|:------|:------|
|["119", "97674223", "1195524421"]|false|
|["123","456","789"]|true|
|["12","123","1235","567","88"]|false|


<br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.Arrays;
class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        Arrays.sort(phone_book);
        
        String temp = phone_book[0];
        for(int i = 1; i < phone_book.length; i++){
            if(phone_book[i].indexOf(temp) == 0) {
                return false; 
            }else {
                temp = phone_book[i];
            }
            
        }
        return answer;
    }
}
```

{% endraw %}



![결과](https://blog.kakaocdn.net/dn/b0oyMC/btq6SkZX2fI/By0VhVQ7kqHNHwD3kXvB60/img.png)




<br><br>


**다른 사람의 풀이** <br>

```java
// 김기준 , 탈퇴한 사용자 , - , okok7028 , - 외 301 명

class Solution {
    public boolean solution(String[] phoneBook) {
       for(int i=0; i<phoneBook.length-1; i++) {
            for(int j=i+1; j<phoneBook.length; j++) {
                if(phoneBook[i].startsWith(phoneBook[j])) {return false;}
                if(phoneBook[j].startsWith(phoneBook[i])) {return false;}
            }
        }
        return true;
    }
}
```

위의 풀이 방법에서는 처음 보는 함수를 발견했다. startsWith()라는 함수인데 이 함수는 비교 대상 문자열이 입력된 문자열 값으로 시작되는지 여부를 확인하고 boolean 값을 리턴한다. <br> 

```java
String str = "안녕하세요";

System.out.println(str.startsWith("안녕")); // true
```

좋은 함수를 알았지만 아쉽게도 위의 코드는 효율성 테스트에서 3, 4 케이스에서 시간 초과가 뜬다. 아마도 내 생각엔 이중 for문을 사용해서 그런 것 같다.

![결과2](https://blog.kakaocdn.net/dn/edR7mO/btq6Q70ZxE6/ZGHY1zwcBf9GrhRbgxKEHk/img.png)

<br> 

또 다른 코드는 나와 같이 정렬로 풀이했는데 나보다 코드를 더 짧게 쓰셨다.

```java
//- , - , 한장호 , 권일우 , 신제문 외 4 명

import java.util.Arrays;

class Solution {
    public boolean solution(String[] phoneBook) {
        Arrays.sort(phoneBook);
        boolean result = true;
        for (int i=0; i<phoneBook.length-1; i++) {
            if (phoneBook[i+1].contains(phoneBook[i])) {
                result = false;
                break;
            }
        }
        return result;
    }
}
```
