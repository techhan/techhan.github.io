---
title: "[프로그래머스] 크레인 인형뽑기 게임(JAVA)"
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

> 게임개발자인 "죠르디"는 크레인 인형뽑기 기계를 모바일 게임으로 만들려고 합니다.<br>
"죠르디"는 게임의 재미를 높이기 위해 화면 구성과 규칙을 다음과 같이 게임 로직에 반영하려고 합니다.<br> ![크레인1](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png) <br><br> 게임 화면은 "1 x 1" 크기의 칸들로 이루어진 "N x N" 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다. (위 그림은 "5 x 5" 크기의 예시입니다). 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다. 모든 인형은 "1 x 1" 크기의 격자 한 칸을 차지하며 격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다. 게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있습니다. 집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다. 다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다. <br><br> ![크레인2](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png) <br><br> 만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다. 위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 두 개가 없어집니다. <br><br> ![크레인3](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif) <br><br> 크레인 작동 시 인형이 집어지지 않는 경우는 없으나 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다. 또한 바구니는 모든 인형이 들어갈 수 있을 만큼 충분히 크다고 가정합니다. (그림에서는 화면표시 제약으로 5칸만으로 표현하였음)<br><br>게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return 하도록 solution 함수를 완성해주세요.
 
<br>

## 제한사항
{: style="margin-bottom:0px; padding-bottom:0px"}
>
- board 배열은 2차원 배열로 크기는 "5 x 5" 이상 "30 x 30" 이하입니다.
- board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
    - 0은 빈 칸을 나타냅니다.
    - 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.
- moves 배열의 크기는 1 이상 1,000 이하입니다.
- moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.

<br>

## 입출력 예

|board|moves|result|
|:------|:------|:------|
|[[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]]|[1,5,3,5,1,2,1,4]|4|


<br>

## JAVA 풀이 과정

{% raw %}

```java
import java.util.ArrayList;

class Solution {
    public int push(int[][] board, int move){
        int num = 0;
        for(int i = 0; i < board.length; i++){
            if(board[i][move-1] != 0) {
                num = board[i][move-1];
                board[i][move-1] = 0;
                return num;
            }
        }
        return 0;
    }

    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        int temp = 0;
        ArrayList<Integer> basket = new ArrayList<>();

        for(int i = 0; i < moves.length; i++){
            temp = push(board, moves[i]);
            if(temp != 0) {
                basket.add(temp);
                for(int k = 0; k < basket.size() - 1; k++){
                    if(basket.get(k) == basket.get(k + 1)) {
                        for(int j = 0; j < 2; j++) basket.remove(k);
                        answer += 2;
                        k = 0;
                    }
                }
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과1](https://user-images.githubusercontent.com/70805241/118309822-c4ccaf80-b528-11eb-86ed-f0c1cd86eebe.png)


처음에는 푸는데 급급해서 효율성이라고는 1도 찾아볼 수 없고, 너무 불필요한 반복이 많았던 코드를 작성했다. 통과를 했다는 뿌듯함은 잠시, `테스트 4`번이 20초를 넘어가는 걸 보고 '아, 이건 뭔가 잘못됐다.'라는 생각으로 코드를 약간 손봤다.


<br><br>

**리팩토링**

{% raw %}

```java
import java.util.ArrayList;

class Solution {
    public int push(int[][] board, int move){
        int num = 0;
        for(int i = 0; i < board.length; i++){
            if(board[i][move-1] != 0) {
                num = board[i][move-1];
                board[i][move-1] = 0;
                return num;
            }
        }
        return 0;
    }
    
    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        int temp = 0;
        ArrayList<Integer> basket = new ArrayList<>();
        
        for(int i = 0; i < moves.length; i++){
            temp = push(board, moves[i]);
            if(temp != 0) {
                if(!basket.isEmpty() && (temp == basket.get(basket.size()-1))) {
                    basket.remove(basket.size()-1);
                    answer += 2;
                } else{
                   basket.add(temp);
                }
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

![결과2](https://user-images.githubusercontent.com/70805241/118309849-cdbd8100-b528-11eb-9a3b-7fefad2265fd.png)


<br>

처음에 작성했던 코드와 다른 점은 temp가 0이 아닐 때 basket에 먼저 넣지 않고, basket 맨 뒤에 있는 값과 temp을 비교해 둘이 같으면 basket의 맨 뒤에 있는 값을 삭제하고 answer에 2를 누적 저장했다. 그리고 같지 않으면 basket에 담았다. Stack을 이용하면 좀 더 짧게 코드를 작성했겠지만 뭔가 그래도 비슷하게 구현은 해보고 싶어서 구구절절 코드를 짜봤다. 

<br><br>


**다른 사람 풀이** <br>

{% raw %}

```java
// 홍희표 , 김재용 , lily , 주익정
import java.util.Stack;

class Solution {
    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        Stack<Integer> stack = new Stack<>();
        for (int move : moves) {
            for (int j = 0; j < board.length; j++) {
                if (board[j][move - 1] != 0) {
                    if (stack.isEmpty()) {
                        stack.push(board[j][move - 1]);
                        board[j][move - 1] = 0;
                        break;
                    }
                    if (board[j][move - 1] == stack.peek()) {
                        stack.pop();
                        answer += 2;
                    } else
                        stack.push(board[j][move - 1]);
                    board[j][move - 1] = 0;
                    break;
                }
            }
        }
        return answer;
    }
}
```

{% endraw %}

<br>

위의 코드는 Stack으로 구현한 코드이다. 확실히 Stack 클래스를 이용해서 풀이하니 코드가 훠어어어얼씬 짧다.