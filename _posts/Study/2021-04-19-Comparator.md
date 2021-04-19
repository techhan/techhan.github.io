---
title:  "Comparable과 Comparator"
excerpt: "객체 정렬하기"
categories: 
  - Study
tags: 
  - Java
toc : true
---


## Comparable
Comparable은 인터페이스이다. 이 인터페이스에는 객체를 정렬하는 데 사용되는 메소드인 `compareTo()` 메서드를 정의하고 있기 때문에 사용자 정의 클래스에서는 이 메서드를 `오버라이딩`하여 사용한다. <br>

- 리턴 타입 : int
- 메서드 : compareTo(T o)
- 주어진 객체와 같으면 0, 적으면 음수, 크면 양수를 리턴한다.
- `Collections.sort()`와 함께 써야 정렬이 완료된다.
- 기본적으로 오름차순 정렬이며, 내림차순을 원한다면 compareTo() 로직을 반대로 변경하면 된다. 

<br>

```java
// Comparable 구현 클래스

public class Person implements Comparable<Person>{
	public String name;
	public int age;
	public int height;
	
	public Person(String name, int age, int height) {
		this.name = name;
		this.age = age;
		this.height = height;
	}
	
	@Override
	public int compareTo(Person o) { // 정렬 기준 : 나이
		if(age < o.age)return -1;
		else if(age == o.age) return 0;
		else return 1;
	}

	@Override
	public String toString() {
		return name + ", " + age + ", " + height;
	}
}
```

```java
import java.util.ArrayList;
import java.util.Collections;

public class PsersonRun {
	public static void main(String[] args) {
		ArrayList<Person> list = new ArrayList<>();
		
		list.add(new Person("고길동", 43, 170));
		list.add(new Person("이선희", 38, 167));
		list.add(new Person("조선우", 23, 165));
		list.add(new Person("이한솔", 28, 168));
		
		Collections.sort(list);
		for(Person p : list) {
			System.out.println(p);
		}
	}
}
```

<br>

**실행 결과** <br>
![결과1](https://user-images.githubusercontent.com/70805241/115212354-608e1a00-a13b-11eb-88f5-fc2b111dba65.png) <br><br>

나이 순으로 정렬이 된 걸 확인할 수 있다. 만약 나이가 아니라 키 순서대로 정렬하고 싶으면 Compareble 구현 클래스 내 compareTo() 메서드 내부 if문 조건을 변경해주면 된다.

```java
// 정렬 기준 : 키
@Override
public int compareTo(Person o) {
    if(height < o.height)return -1;
    else if(height == o.height) return 0;
    else return 1;
}
```

<br>

**실행 결과** <br>

![결과2](https://user-images.githubusercontent.com/70805241/115212599-a6e37900-a13b-11eb-9a89-a6e2fee71ce3.png) <br>

compareTo() 메서드의 경우는 문자열은 정렬할 수 없고, 비교만 가능하다.


<br><br>

-----------

<br><br>

## Comparator
Comparator 인터페이스도 객체를 정렬하는 데 사용되는 인터페이스이다.
Comparator 인터페이스를 구현하면 오름차순 이외의 기준으로도 정렬할 수 있다. Comparator는 `compare()` 메서드를 재정의하여 사용한다. <br>


- 리턴 타입 : int
- 메서드 : compare(T o1, T o2)
- 비교하는 두 객체가 동등하면 0, 비교하는 값보다 앞에 오게 하려면 음수, 뒤에 오게 하려면 양수를 리턴


<br>

**[프로그래머스] 문자열 내 마음대로 정렬**

```java
import java.util.Arrays;
import java.util.Comparator;

public class compareSort {
	public static String[] solution(String[] strings, int n) {
		Arrays.sort(strings, new Comparator<String>() {
			@Override
			public int compare(String o1, String o2) {
				if(o1.charAt(n) > o2.charAt(n)) return 1;
				else if(o1.charAt(n) == o2.charAt(n)) return o1.compareTo(o2);
				else return -1;
			}
		});
		return strings;
	}
	
	public static void main(String[] args) {
		System.out.println(Arrays.toString(solution(new String[] {"abce", "abde", "cdx"}, 1)));
	}
}
```

**실행 결과** <br><br>

![결과3](https://user-images.githubusercontent.com/70805241/115220501-946d3d80-a143-11eb-83e0-7d074c13076c.png)