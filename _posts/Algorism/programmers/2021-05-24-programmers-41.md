---
title: "[프로그래머스] 비밀지도(JAVA)"
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

네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.<br>

1. 지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 "공백"(" ") 또는 "벽"("#") 두 종류로 이루어져 있다.
2. 전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 "지도 1"과 "지도 2"라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
3. "지도 1"과 "지도 2"는 각각 정수 배열로 암호화되어 있다.
4. 암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다.

![비밀지도1](https://user-images.githubusercontent.com/70805241/119364057-79b15a00-bce9-11eb-8c4c-df5e6d19c6cd.png)


네오가 프로도의 비상금을 손에 넣을 수 있도록, 비밀지도의 암호를 해독하는 작업을 도와줄 프로그램을 작성하라.


<br>

> ## 입력 형식
{: style="margin-bottom:0px; padding-bottom:0px"}

- 1 ≦ n ≦ 16
- arr1, arr2는 길이 n인 정수 배열로 주어진다.
- 정수 배열의 각 원소 x를 이진수로 변환했을 때의 길이는 n 이하이다. 즉, 0 ≦ x ≦ 2n - 1을 만족한다.

<br>


> ## 출력 형식
{: style="margin-bottom:0px; padding-bottom:0px"}

원래의 비밀지도를 해독하여 '#', 공백으로 구성된 문자열 배열로 출력하라.

<br>


> ## 입출력 예

|매개변수|값|
|:------|:------|
|n|5|
|arr1|[9, 20, 28, 18, 11]|
|arr2|[30, 1, 21, 17, 28]|
|출력|["#####","# # #", "### #", "# ##", "#####"]|

<br>

|매개변수|값|
|:------|:------|
|n|6|
|arr1|[46, 33, 33 ,22, 31, 50]|
|arr2|[27 ,56, 19, 14, 14, 10]|
|출력|["######", "### #", "## ##", " #### ", " #####", "### # "]|




<br>

> ## JAVA 풀이 과정

{% raw %}

```java
class Solution {
    public String decoding(int n1, int n2, int n){
        String zero = "";
        String s = Integer.toBinaryString(n1 | n2);
        if(s.length() < n) {
            for(int i = s.length(); i < n; i++){
                zero += "0";
            }
        }
        return zero + s;
    }
    
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        for(int i = 0; i < n; i++){
            answer[i] = decoding(arr1[i], arr2[i], n);
            answer[i] = answer[i].replaceAll("[1]", "#");
            answer[i] = answer[i].replaceAll("[0]", " ");
        }
        return answer;
    }
}
```

{% endraw %}

<br>


![결과](https://user-images.githubusercontent.com/70805241/119364582-00fecd80-bcea-11eb-972e-f362aa60b424.png)


<br>

처음에 코드를 제출했을 때 첫 번째 테스트 케이스만 맞고, 두 번째 테스트 케이스는 통과하지 못했다. <br>

![실패요인](https://user-images.githubusercontent.com/70805241/119365350-ccd7dc80-bcea-11eb-8701-e93d3d2407d2.png) <br>

배열 중 4번째 배열, 5번째 배열이 한 칸씩 밀려있는 걸 보고 for문을 돌려 replaceAll()을 하기 전 answer를 출력해봤다. 

![실패요인2](https://user-images.githubusercontent.com/70805241/119365685-27713880-bceb-11eb-9d0c-955e0acf266b.png)

<br>

문제에 나와있는 입력 형식에 밑의 조건을 간과했다. 

```
정수 배열의 각 원소 x를 이진수로 변환했을 때의 길이는 n 이하이다. 즉, 0 ≦ x ≦ 2n - 1을 만족한다.
```

<br>

어떻게 앞에 0을 붙일까 고민하다가 메서드를 따로 선언해서 s의 길이가 n보다 짧으면 맨 앞에 0을 붙이는 로직을 짜서 통과했다. 


<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
//  - , - , 김수호 , nanana , 김평안 외 3 명
class Solution {
  public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] result = new String[n];
        for (int i = 0; i < n; i++) {
            result[i] = Integer.toBinaryString(arr1[i] | arr2[i]);
        }

        for (int i = 0; i < n; i++) {
            result[i] = String.format("%" + n + "s", result[i]);
            result[i] = result[i].replaceAll("1", "#");
            result[i] = result[i].replaceAll("0", " ");
        }

        return result;
    }
}
```

{% endraw %}

<br>

위의 코드는 문자열의 길이를 맞추는 방식을 `String.format()` 메서드를 사용해서 구현했다. %s 이런 문자 표현 방식을 System.out.printf() 할 때만 써봐서 저렇게 사용할 수 있을 줄 몰랐다.... String.format() 잊지말자악