---
title:  "[알유] 재귀 함수 - 1"
excerpt: "팩토리얼"
categories: 
  - Study
tags: 
  - Java
toc : true
---

<br>

## 재귀란?
재귀(Recursion)는 자신을 정의할 때 자기 자신을 재참조하는 방법을 뜻한다. 


<p align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/Screenshot_Recursion_via_vlc.png/1024px-Screenshot_Recursion_via_vlc.png" height="500px" width="500px" title="출처 : 위키백과">
</p>

<br>

재귀를 효과적으로 사용하면 프로그램을 간결하게 만들 수 있다. <br>

<br><br>

-----------

<br>

### 팩토리얼 구하기
음이 아닌 정수 n의 팩토리얼 (n!)은 아래처럼 재귀적으로 정의할 수 있다. 

```
1. 0!=1
2. n > 0이면 n! = n x (n - 1)
```


<br>

팩토리얼 함수 부분을 코드로 작성해보면 아래와 같다. <br>

```java
static int factorial(int n) {
    if(n > 0)
        return n * factorial(n - 1);
    else
        return 1;
}
```

<br>

factorial 메서드는 매개변수 n에 전달받은 값이 0보다 크면 n * factorial(n-1)을 반환하고, 그렇지 않으면 1을 반환한다. <br>
<br>

위와 같은 방법으로 factorial(3)을 이용해 팩토리얼 값 6을 얻을 수 있다. factorial 메서드는 n - 1의 팩토리얼 값을 구하기 위해 다시 factorial 메서드를 호출한다. 이러한 메서드 호출 방식을 재귀 호출(recursive call)이라고 한다. <br>

<br>

사실 이론상으로는 이해를 했는데 재귀 함수가 동작하는 방식에 대해서는 아직까지는 100퍼센트 이해하지 못했다. 그래도 그나마 제일 쉽게 이해할 수 있는 설명은 [여기](https://marobiana.tistory.com/79) 이 블로그이다.. 계속 계속 들여다보면 언젠간 이해할 수 있겠지. <br>