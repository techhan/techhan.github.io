---
title:  "[알유]선형 검색"
excerpt: "검색 알고리즘"
categories: 
  - Study
tags: 
  - Java
toc : true
---

## 선형 검색
> 리스트에서 특정한 값을 만날 때까지 맨 앞부터 순서대로 요소를 검색하는 알고리즘이며 선형 검색 또는 순차 검색이라고 불린다.

<br>



<p align="center"><img src="https://user-images.githubusercontent.com/70805241/117855222-3b697300-b2c5-11eb-9aad-d2a3cc0a6fc7.png" height="450px" width="450px">
</p>

<br><br>

위의 경우는 검색이 성공한 경우이며, 만약 배열 값에 '4'가 없었다면 배열의 맨 마지막까지 탐색하고 검색을 종료한다. 즉, 검색의 `종료 조건`은 두 개이다. <br>

1. 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우 (실패)
2. 검색할 값과 같은 요소를 발견한 경우 (성공)

<br>

배열의 요솟수가 n개일 때 조건 1, 2를 판단하는 횟수는 평균 `n/2회`이다.

<br><br> 



### 적용하기(프로그래머스 : 서울에서 김서방 찾기)
[프로그래머스로 이동](https://programmers.co.kr/learn/courses/30/lessons/12919) <br>


**기존 작성 코드** <br>

```java
class Solution {
    public String solution(String[] seoul) {
        String answer = "";
        
        for(int i = 0; i < seoul.length; i++){
            if(seoul[i].equals("Kim")){
                answer = "김서방은 " + i + "에 있다";
                break;
            }
        }
        return answer;
    }
}
```

<br><br>

**리팩토링** <br>

```java
class Solution {
    public String solution(String[] seoul) {        
        for(int i = 0; i < seoul.length; i++){
            if(seoul[i].equals("Kim")){
                return "김서방은 " + i + "에 있다";
            }
        }
        return "";
    }
}
```


<br><br>

---------

<br><br>



## 보초법(sentinel method)
>선형 검색은 반복할 때마다 위에서 말했던 종료 조건 1과 2를 모두 판단한다. 종료 조건을 검사하는 비용을 반으로 줄이는 방법을 보초법이라고 한다.

<br>

<p align="center"><img src="https://user-images.githubusercontent.com/70805241/117859171-a0bf6300-b2c9-11eb-9836-b5d8a937dc8d.png" height="450px" width="450px">
</p>


위의 그림처럼 기존에 있던 원래 데이터 뒤에 검색하고자 하는 키 값을 맨 끝 요소에 저장한다. 이때 저장하는 값을 보초(sentinel)라고 한다. 두 번째 상황처럼 원하는 값이 원래의 데이터에 존재하지 않아도 보초인 5번째 index까지 검색하면 종료 조건 2번이 성립된다. 이렇게하면 보초는 반복문에서 종료 판단 횟수를 `2회에서 1회로 줄이는 역할`을 한다.

<br>


### 적용하기

위 사진과 같은 배열 int[] a, 배열의 길이인 n, 검색할 값이 담긴 변수 key가 매개 변수로 주어질 때 아래와 같이 구현할 수 있다.

```java
class Solution {
    public String solution(int[] a, int n, int key) {
        int i = 0;
        a[n] = key; // 보초 추가
        while(true) {
            if(a[i] == key) break;
            i++;
        }
        return i == n ? -1 : i;
    }
}
```