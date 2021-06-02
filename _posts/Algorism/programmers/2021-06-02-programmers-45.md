---
title: "[프로그래머스] JadenCase 문자열 만들기(JAVA)"
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

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

<br><br>


> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- s는 길이 1 이상인 문자열입니다.
- s는 알파벳과 공백문자(" ")로 이루어져 있습니다.
- 첫 문자가 영문이 아닐때에는 이어지는 영문은 소문자로 씁니다. ( 첫번째 입출력 예 참고 )
<br>

> ## 입출력 예

|s|result|
|:------|:------|
|"3people unFollowed me"|"3people Unfollowed Me"|
|"for the last week"|"For The Last Week"|

<br>

> ## JAVA 풀이 과정

{% raw %}

```java

class Solution {
    public String solution(String s) {
        String answer = "";
        StringBuffer sb = new StringBuffer();
        
        String[] temp = s.toLowerCase().split(" ");
        
        for(int i = 0; i < temp.length; i++){
            if(temp[i].length() == 1)
                sb.append(Character.toUpperCase(temp[i].charAt(0)));
            else{
            sb.append(Character.toUpperCase(temp[i].charAt(0)) 
                     + temp[i].substring(1));
            }
            if(i != temp.length - 1) sb.append(" ");
        } 
        return sb.toString();
    }
}
```

{% endraw %}

<br>


![결과](https://lh3.googleusercontent.com/bZNwt1aRwKbre07CKlH6FFrJ0lf1ne3UCn8IOZzNR-cusSFV8zNsjBER_3hfbcVSsrH6MxYv62Kt1wGzL1NXRgAkCNqe-LpSHCw-lJtsySzI0C0i86yPCv_sE2AbDCD_KMtXxg6r5Jat9cIBwJha9zlfuICoMYoHXya9nxjjrACL99hkCPYUs-v0Yao_MH6XdCUQFk3GgCqvrnE_8rolsc3sED_RSHzY6ssjqfTfxQuVnazjFlk2jiLvhfCebpkEAqIso-Y4vtlwCDQwzT78lasTv1h2ZAPChMF4Y9t4l7qWsLE0W5BM5wXqKbzDsTVMFXitaiqj1ZyqX-tGrNgpQ_o1ZT-I94FRRWS_kPiHzGsPDFE9SKb6n916DMXzGUtN47rwQi1VIUEUcxUKxPmivp_SwQfZaT76DgfIPoX7N-lCnqdfgdbQeJy77fjlzXDmzXn81pNTGpGcMJ_p3UqoitWnPNOItvOE6VwRz2RicIkRXcKIE4gMR3RVVuUfAw509hZpgS6wd8k-HK5MxhNGjtov3QpdMab2AvUzgdVWH5GD-2lFgt2qcKzldFXROhhb9j9xmDjmqtN9jQt2F5KTTRfJNr9zn4hNfGr4l0hMV4B91x1ZQ9o46mkLkLfoKONpUTuU_rcFPiLYdVRKLkKluQCY3q-lXZYmgHbfJ5MZjbj4AemweCk0wWFjpUL-V0aJmuv_aasWW7uemP2-FJLf1PA=w390-h432-no?authuser=0) <br>


제일 처음 작성했던 코드다. 테스트 케이스 두 개 모두 통과했지만 제출하면 '런타임 에러'가 발생하면서 계속 통과하지 못했다. 그래서 아예 방법을 좀 바꿨다.  <br><br>

----------------

<br>

**두 번째 풀이** <br>

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        
        StringBuffer sb = new StringBuffer();
        s = s.toLowerCase();
        sb.append(Character.toUpperCase(s.charAt(0)));
        for(int i = 1; i < s.length(); i++){
            if(s.charAt(i) == ' ') sb.append(" ");
            else if(s.charAt(i - 1) == ' ')
                sb.append(Character.toUpperCase(s.charAt(i)));
            else sb.append(s.charAt(i));
        }
        return sb.toString();
    }
}
```
<br>


![결과2](https://user-images.githubusercontent.com/70805241/120469833-d5609f00-c3dd-11eb-89b6-10af9459ef0f.png)


<br>

이번 문제에서 주의해야할 점은 바로 `공백`이었다. 공백이 하나가 올 수도, 여러 개가 올 수도 있다는 걸 처음엔 생각도 못했다. 그냥 예시처럼 공백은 무조건 하나가 올 줄 알았는데..^^ 아무튼 공백만 신경쓴다면 그리 어렵지 않게 풀이할 수 있을 정도의 문제였다.  <br>



<br><br>


**다른 사람의 풀이** <br>

```java
// Sunhee Shin , 조희준 , LimHanGyeol , wonsangki , 모아나 외 9 명
class Solution {
  public String solution(String s) {
        String answer = "";
        String[] sp = s.toLowerCase().split("");
        boolean flag = true;

        for(String ss : sp) {
            answer += flag ? ss.toUpperCase() : ss;
            flag = ss.equals(" ") ? true : false;
        }

        return answer;
  }
}

```

<br> 

코드를 보고 진짜로 놀랐다. 엄청 짧고 단순한 코드다. sp라는 String 배열에 문자열 s의 모든 글자를 소문자로 만들고 split()을 사용해 sp에 담았다. 그리고 flag를 하나 선언했다. <br>
for문에서는 answer에 누적 저장을 하는데, flag가 true이면 ss문자열을 대문자로, 아니면 소문자인 상태로 대입한다. 그리고 flag에 ss가 공백이면 true를 대입, 아니면 false로 대입하게 했다. <br>
