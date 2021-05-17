---
title: "[프로그래머스] 시저 암호(JAVA)"
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

> 어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.


<br>

## 입출력 예

|s|n|result|
|:------|:------|:------|
|"AB"|1|"BC"|
|"z"|1|"a"|
|"a B z"|4|"e F d"|


<br>

## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public String solution(String s, int n) {
        char[] arr = s.toCharArray();
        
        for(int i = 0; i < arr.length; i++){
            if(arr[i] != ' '){
                if(Character.isUpperCase(arr[i])){
                     arr[i] += n;
                    if(arr[i] > 'Z') {
                    arr[i] = (char)('A' + (arr[i] - 'Z' -1));
                    }
                } else {
                     arr[i] += n;
                    if(arr[i] > 'z'){
                        arr[i] = (char)('a' + (arr[i] - 'z' - 1));
                    }
                }
            }
        }
        return String.valueOf(arr);
    }
}
```

{% endraw %}

<br>

![결과](https://user-images.githubusercontent.com/70805241/118518012-b2de4d00-b772-11eb-82fc-e3fb947a62df.png)



일단 매개 변수로 들어오는 문자열 s를 char 배열에 담았다. 그리고 for문을 char 배열의 길이 만큼 돌린다. `공백`은 밀어도 밀어도 공백이니 공백이 아닐 때만 매개 변수로 들어오는 'n'만큼 더해준다. 근데 알파벳 소문자, 대문자를 따로 연산해야하니 먼저 `Character.isUpperCase()`로 대문자인지, 소문자인지 판별하여 그 안에 연산 부분을 구현했다. 이 문제에서 난이도가 있었던 건 연산 결과가 'z'나 'Z'를 넘어서는 부분이다. 나는 일단 arr[i]에 있는 값을 n만큼 더하고, arr[i]가 'z'나 'Z'보다 크면 ''A(a)' + (arr[i] - 'Z(z)' - 1)'를 해줬다.

<br><br>





**다른 사람 풀이** <br>

{% raw %}

```java
// Isaac Ahn , 문하 , - , - , Sung Rak 외 31 명
// 문제가 개편되었습니다. 이로 인해 함수 구성이나 테스트케이스가 변경되어, 과거의 코드는 동작하지 않을 수 있습니다.
// 새로운 함수 구성을 적용하려면 [코드 초기화] 버튼을 누르세요. 단, [코드 초기화] 버튼을 누르면 작성 중인 코드는 사라집니다.
class Caesar {
    String caesar(String s, int n) {
        String result = "";
    n = n % 26;
    for (int i = 0; i < s.length(); i++) {
      char ch = s.charAt(i);
      if (Character.isLowerCase(ch)) {
        ch = (char) ((ch - 'a' + n) % 26 + 'a');
      } else if (Character.isUpperCase(ch)) {
        ch = (char) ((ch - 'A' + n) % 26 + 'A');
      }
      result += ch;
    }
        return result;
    }

    public static void main(String[] args) {
        Caesar c = new Caesar();
        System.out.println("s는 'a B z', n은 4인 경우: " + c.caesar("a B z", 4));
    }
}
```

{% endraw %}

<br>

위의 코드는 char 배열을 따로 만들지 않고 `charAt()`을 이용해 변환한 값을 String 타입의 result에 담았다. 그리고 문자 연산 부분에서 `(char) ((ch - 'a' + n) % 26 + 'a');` 부분이 흥미로웠다. 