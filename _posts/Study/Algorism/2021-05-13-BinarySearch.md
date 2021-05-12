---
title:  "[알유]이진 검색"
excerpt: "검색 알고리즘"
categories: 
  - Study
tags: 
  - Java
toc : true
---

## 이진 검색
> 이진 검색(Binary Search)은 오름차순 또는 내림차순으로 `정렬`된 리스트에서 특정한 값의 위치를 찾는 알고리즘이다. 이진 검색은 후보 범위가 한 항목으로 좁아질 때까지 찾고자 하는 항목을 포함하고 있는 리스트를 반으로 나누는 과정을 반복한다. 선형 검색보다 속도적인 측면에서 더 빠르지만 정렬된 리스트에만 사용할 수 있다는 단점이 있다.

<br>



<p align="center"><img src="https://user-images.githubusercontent.com/70805241/118007703-f570e580-b37e-11eb-818c-4d23aabc03b6.png" height="500px" width="500px">
</p>

<br><br>

제일 처음 검색을 시작할 때 중앙에 위치한 5번 인덱스에 있는 값을 검색하려는 값 '39'와 비교한다. 31 < 39가 성립되므로 0번 인덱스부터 5번 인덱스까지는 검색 범위에서 제외한다. <br>그 다음 비교는 나머지 6번 인덱스와 10번 인덱스의 중앙인 8번 인덱스와 비교한다. 68 > 39가 성립되므로 8번 인덱스부터 10번 인덱스를 검색 범위에서 제외한다. <br>그리고 6번, 7번 인덱스 중앙 값은 (6+7)/2로 계산되기 때문에 6번 인덱스를 39와 비교한다. 39 == 39가 성립되므로 검색을 성공하고 종료한다.

<br>

### 적용하기[(백준 : 수 찾기)](https://techhan.github.io/algorithm/baekjoon-2/)

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		int[] aArr = new int[n];
		
		for(int i = 0; i < n; i++) {
			aArr[i] = sc.nextInt();
		}
		
		int m = sc.nextInt();
		int[] keyArr = new int[m];
		
		for(int i = 0; i < m; i++) {
			keyArr[i] = sc.nextInt();
		}
		
		Arrays.sort(aArr);	
		
		for(int i = 0; i < m; i++) {
			System.out.println(biSearch(aArr, keyArr[i]));
		}
	}
	
    // 이분 탐색 메서드
	public static int biSearch(int[] nArr, int key) {
		int low = 0; // 검색 범위 첫 인덱스
		int high = nArr.length - 1; // 검색 범위의 끝 인덱스
		int mid = 0; // 검색 범위 중간 인덱스
		
		while(low <= high) {
			mid = (low + high) / 2;
			if(nArr[mid] == key) return 1; // 검색 성공 시 0 반환
                // 중앙 값이 검색 값보다 작으면 low에 중앙 인덱스 + 1 한 값 대입
			else if(nArr[mid] < key) low = mid + 1; 
                // 중앙 값이 검색 값보다 크면 high에 중앙 인덱스 값 - 1 한 값 대입
			else high = mid - 1; 
		}
		return 0; // 검색 실패 시 0 반환
	}
}
```


<br><br>

- 참고 : Do it 자료구조와 함께 배우는 알고리즘 입문 자바 편