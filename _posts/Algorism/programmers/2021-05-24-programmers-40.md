---
title: "[프로그래머스] 신규 아이디 추천(JAVA)"
excerpt: "Level 1"
categories: 
  - Algorithm
tags: 
  - Programmers
  - JAVA
  - Level_1
---
 
> ## 문제 설명
{: style="margin-bottom:0px; padding-bottom:0px"}

카카오에 입사한 신입 개발자 네오는 "카카오계정개발팀"에 배치되어, 카카오 서비스에 가입하는 유저들의 아이디를 생성하는 업무를 담당하게 되었습니다. "네오"에게 주어진 첫 업무는 새로 가입하는 유저들이 카카오 아이디 규칙에 맞지 않는 아이디를 입력했을 때, 입력된 아이디와 유사하면서 규칙에 맞는 아이디를 추천해주는 프로그램을 개발하는 것입니다. <br>
다음은 카카오 아이디의 규칙입니다.
- 아이디의 길이는 3자 이상 15자 이하여야 합니다.
- 아이디는 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.) 문자만 사용할 수 있습니다.
- 단, 마침표(.)는 처음과 끝에 사용할 수 없으며 또한 연속으로 사용할 수 없습니다.

"네오"는 다음과 같이 7단계의 순차적인 처리 과정을 통해 신규 유저가 입력한 아이디가 카카오 아이디 규칙에 맞는 지 검사하고 규칙에 맞지 않은 경우 규칙에 맞는 새로운 아이디를 추천해 주려고 합니다. <br>
신규 유저가 입력한 아이디가 new_id 라고 한다면,
```
1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
     만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
```
<br>
신규 유저가 입력한 아이디를 나타내는 new_id가 매개변수로 주어질 때, "네오"가 설계한 7단계의 처리 과정을 거친 후의 추천 아이디를 return 하도록 solution 함수를 완성해 주세요.


<br>

> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- new_id는 길이 1 이상 1,000 이하인 문자열입니다.
- new_id는 알파벳 대문자, 알파벳 소문자, 숫자, 특수문자로 구성되어 있습니다.
- new_id에 나타날 수 있는 특수문자는 -_.~!@#$%^&*()=+[{]}:?,<>/ 로 한정됩니다.


<br>

> ## 입출력 예

|no|new_id|result|
|:------|:------|:------|
|예1|"...!@BaT#*..y.abcdefghijklm"|"bat.y.abcdefghi"|
|예2|"z-+.^."|"z--"|
|예3|"=.="|"aaa"|
|예4|"123_.def"|"123_.def"|
|예5|"abcdefghijklmn.p"|"abcdefghijklmn"|



<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public String solution(String new_id) {
        String answer = new_id.toLowerCase();
        
        answer = answer.replaceAll("[^0-9a-z-_.]", "");
        answer = answer.replaceAll("[.]{2,}", ".");
        answer = answer.replaceAll("^[.]{1}", "");
        
        if(answer.equals(""))  answer += "a";
 
        
        if(answer.length() >= 16) answer = answer.substring(0, 15);
        
        answer = answer.replaceAll("[.]{1}$", "");
       
        
        if(answer.length() <= 2) {
            for(int i = answer.length(); i < 3; i++){
                answer += answer.substring(answer.length()-1);
            }
        }

        return answer;
    }
}
```

{% endraw %}

<br>


![결과](https://user-images.githubusercontent.com/70805241/119272829-93479880-bc3a-11eb-8f0f-3d7d46a0fadc.png)


<br>

처음에 코드를 제출했을 때 계속 테스트 케이스 22,23에서 실패가 떴다. 테스트 케이스를 이것저것 추가해봤는데도 모르겠어서 문제를 다시 읽어보며 코드를 훑어보니까 `5단계`가 문제였다. 문제에서 나오는 테스트 케이스 3번의 "aaa"를 보고 코드를 작성해서 a만 대입하는 게 아닌, for문을 돌려 new_id의 길이만큼 반복시킨 게 문제였다. 해당 부분을 고치니 통과되었다. 


<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
//  -
class Solution {
    public String solution(String new_id) {

        String s = new KAKAOID(new_id)
                .replaceToLowerCase()
                .filter()
                .toSingleDot()
                .noStartEndDot()
                .noBlank()
                .noGreaterThan16()
                .noLessThan2()
                .getResult();


        return s;
    }

    private static class KAKAOID {
        private String s;

        KAKAOID(String s) {
            this.s = s;
        }

        private KAKAOID replaceToLowerCase() {
            s = s.toLowerCase();
            return this;
        }

        private KAKAOID filter() {
            s = s.replaceAll("[^a-z0-9._-]", "");
            return this;
        }

        private KAKAOID toSingleDot() {
            s = s.replaceAll("[.]{2,}", ".");
            return this;
        }

        private KAKAOID noStartEndDot() {
            s = s.replaceAll("^[.]|[.]$", "");
            return this;
        }

        private KAKAOID noBlank() {
            s = s.isEmpty() ? "a" : s;
            return this;
        }

        private KAKAOID noGreaterThan16() {
            if (s.length() >= 16) {
                s = s.substring(0, 15);
            }
            s = s.replaceAll("[.]$", "");
            return this;
        }

        private KAKAOID noLessThan2() {
            StringBuilder sBuilder = new StringBuilder(s);
            while (sBuilder.length() <= 2) {
                sBuilder.append(sBuilder.charAt(sBuilder.length() - 1));
            }
            s = sBuilder.toString();
            return this;
        }

        private String getResult() {
            return s;
        }
    }
}
```

{% endraw %}

<br>

정규식을 사용해서 풀이한 건 똑같은데 차이점은 각 단계별로 메서드를 선언해서 풀이했다.