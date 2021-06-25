----
title: "[프로그래머스] 프린터 (JAVA)"
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

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다. 그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다. 이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다. 이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.<br>

```
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
```

<br>

예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.<br>

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.<br>

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

<br>

<br><br>

> ## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}

- 현재 대기목록에는 1개 이상 100개 이하의 문서가 있습니다.
- 인쇄 작업의 중요도는 1~9로 표현하며 숫자가 클수록 중요하다는 뜻입니다.
- location은 0 이상 (현재 대기목록에 있는 작업 수 - 1) 이하의 값을 가지며 대기목록의 가장 앞에 있으면 0, 두 번째에 있으면 1로 표현합니다.

<br>
<br>

> ## 입출력 예

| priorities         | location | return |
| :----------------- | :------- | :----- |
| [2, 1, 3, 2]       | 2        | 1      |
| [1, 1, 9, 1, 1, 1] | 0        | 5      |

<br><br>

> ## JAVA 풀이 과정

{% raw %}

```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.Arrays;

class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 0;
        Queue<Integer> que = new LinkedList<>();

        for(int p : priorities) que.add(p);

        Arrays.sort(priorities);
        int len = priorities.length-1;

        while(!que.isEmpty()){
            int curr = que.poll();

            if(curr == priorities[len - answer]){
                answer++;
                location--;
                if(location < 0) break;
            }else {
                que.add(curr);
                location--;
                if(location < 0) location = que.size()-1;
            }
        }
        return answer;
    }
}
```

{% endraw %}

![결과](https://user-images.githubusercontent.com/70805241/123443075-84c11800-d610-11eb-869b-6d2bac749efb.png)

<br>

오늘은 하다가 막혀서 약간의 힌트를 좀 얻어서 풀이했다 ㅎㅎ..

<br><br>

**다른 사람의 풀이** <br>

```java
//최재웅
import java.util.LinkedList;

class Solution {
     public int solution(int[] priorities, int location) {
        if (priorities.length == 1) {
            return 1;
        }
        int answer = 1;
        LinkedList<Paper> papers = new LinkedList<>();
        for (int i = 0; i < priorities.length; i++) {
            papers.addLast(new Paper(i, priorities[i]));
        }

        while (true) {
            Paper paper = papers.removeFirst();
            for (Paper item : papers) {
                if (paper.priority < item.priority) {
                    papers.addLast(paper);
                    paper = null;
                    break;
                }
            }
            if (paper != null) {
                if (paper.item == location) {
                    return answer;
                } else {
                    answer++;
                }
            }
        }
    }


    class Paper {
        int item;
        int priority;

        public Paper(int item, int priority) {
            this.item = item;
            this.priority = priority;
        }
    }
}

```

ArrayList만을 이용해서 풀이한 코드다.
