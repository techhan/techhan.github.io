---
title: "[프로그래머스] 문자열을 정수로 바꾸기(JAVA)"
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

> 문자열 s를 숫자로 변환한 결과를 반환하는 함수, solution을 완성하세요.
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
> s의 길이는 1 이상 5이하입니다.<br>
s의 맨앞에는 부호(+, -)가 올 수 있습니다.<br>
s는 부호와 숫자로만 이루어져있습니다.<br>
s는 "0"으로 시작하지 않습니다.
<br>

## 입출력 예

예를들어 str이 "1234"이면 1234를 반환하고, "-1234"이면 -1234를 반환하면 됩니다.
str은 부호(+,-)와 숫자로만 구성되어 있고, 잘못된 값이 입력되는 경우는 없습니다.
<br>

## JAVA 풀이 과정

```java
class Solution {
    public int solution(String s) {
        int n = 0;
        return n = Integer.parseInt(s);
    }
}
```

<br>

![결과](https://user-images.githubusercontent.com/70805241/115830835-c9cba100-a44b-11eb-911b-2e5af209dc33.png)




<br>

`음수`를 보고 어떻게 변환할지 고민하다가 프로젝트 때 사용한 `Integer.parseInt()` 메소드를 사용했다! parseInt는 문자열을 int형으로 변환하는 메서드다.

<br><br>

**다른 사람 풀이** <br>

```java
// -
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
public class StrToInt {
    public int getStrToInt(String str) {
            boolean Sign = true;
            int result = 0;

      for (int i = 0; i < str.length(); i++) {
                char ch = str.charAt(i);
                if (ch == '-')
                    Sign = false;
                else if(ch !='+')
                    result = result * 10 + (ch - '0');
            }
            return Sign?1:-1 * result;
    }
    //아래는 테스트로 출력해 보기 위한 코드입니다.
    public static void main(String args[]) {
        StrToInt strToInt = new StrToInt();
        System.out.println(strToInt.getStrToInt("-1234"));
    }
}

```

<br>

위의 코드는 대략적으로 parsInt를 뜯어서 작성한 코드인 것 같다. 

