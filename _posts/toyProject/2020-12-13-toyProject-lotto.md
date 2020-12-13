---
title: "[JavaScript] 로또 당첨 번호"
excerpt: "간단하게 만들어본 로또 당첨 번호 프로그램"
search: true
categories: 
  - ToyProject
tags: 
  - toyProject
  - Javascript
  - CSS
  - HTML
  - VSCODE
---

# 참고 페이지
![20201213_1](https://user-images.githubusercontent.com/70805241/102009328-14406100-3d7a-11eb-9c60-759c06be9d23.JPG "출처: 로또 홈페이지")

<br><br>


# 구현 페이지
![20201213_2](https://user-images.githubusercontent.com/70805241/102009408-929d0300-3d7a-11eb-9f98-d0017e1c9105.gif)
<br><br>

# 구현 코드
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>10_연습문제_1</title>
    <style>
        .areaW{
            width : 520px;
            height: 80px;
            background-color: #fafafa;
            border-radius: 20px;
            float : left;
            position: relative;
        }

        .area1{
            /* padding : 30px; */
            margin : 10px;
            width : 60px;
            height : 60px;
            
            box-sizing: border-box;
            display : inline-block;
            border-radius: 100px;
            position: relative;

        }

        .num{
            box-sizing: border-box;
            padding : 0;
            margin: 0; 
            font-size : 22px;
            line-height: 60px;
            text-align: center; 
            color : #fff;
            text-shadow : 0px 0px 3px rgba(73, 57, 0, .8);
            font-weight:bold;

        }

        .plus{
            width : 90px;
            height : 30px;
            display: inline-block;
            box-sizing: border-box;
            font-size: 50px;
            text-align:center;
            color : #999;
        }

        .bonus{
            padding : 0;
            margin : 0;
            width : 80px;
            height: 80px;
            display: inline-block;
            background-color: #fafafa;
            border-radius: 20px;
        }
        

        #text1 {
            margin : 0;
            width : 520px;
            height : 20px;
            display: inline-block;
            box-sizing: border-box;

        }

        #preText {
            padding : 0;
            margin : 0;
            text-align: center;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        }

        #text2{
            margin-left : 92px;
            width : 80px;
            height : 20px;
            display: inline-block;
            
        }
        #preText2 {
            padding : 0;
            margin: 0;
            text-align: center;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        }
    </style>
</head>
<body>
    <h3>로또 생성기</h3>

    <div class="areaW">
        <!-- 공 번호 영역 -->
        <div class ="area1"><p class="num"></p></div>
        <div class ="area1"><p class="num"></p></div>
        <div class ="area1"><p class="num"></p></div>
        <div class ="area1"><p class="num"></p></div>
        <div class ="area1"><p class="num"></p></div>
        <div class ="area1"><p class="num"></p></div>
    </div>
    
    <!-- '+' 글자 영역 -->
    <div class="plus">+</div>
    
    <!-- 보너스 영역 -->
    <div class="bonus">
        <!-- 보너스 공 번호 영역 -->
        <div class ="area1"><p class="num"></p></div>
    </div>

    <br>
    <!-- 글자 영역 -->
    <div id="text1"><pre id="preText">당첨번호</pre></div>
    <div id="text2"><pre id="preText2">보너스</pre></div>
    
    <br><br>
    <!-- 당첨 번호 버튼 -->
    <button type="button" id="lottoBtn">당첨번호</button>

    <script>
        document.getElementById("lottoBtn").onclick = function() {
            var area1 = document.getElementsByClassName("area1");
            var p = document.getElementsByClassName("num");

            /* 로또 번호를 담을 배열 */
            var numArr = [];

            /* 로또 번호 중복 검사 */
            for(var i = 0; i < area1.length; i++){
                var flag = true;
                var number = parseInt(Math.random() * 45 + 1);
                for(var j = 0; j < i; j++){
                    if(numArr[j] == number){
                        i--;
                        flag = false;
                    }
                }

                /* 로또 번호 정렬 */
                numArr.sort(function(a, b){return a-b;});

                if(flag){
                    numArr[i] = number;
                }
            }

            /* 번호 범위에 따른 색 지정 */
            for(var i = 0; i < area1.length; i++){
                p[i].innerHTML = numArr[i];

                if(numArr[i] <= 10) {
                    area1[i].style.backgroundColor = "#fbc400";
                }
                else if(numArr[i] <= 20){
                    area1[i].style.backgroundColor = "#69c8f2";
                }
                else if(numArr[i] <= 30){
                    area1[i].style.backgroundColor = "#ff7272";
                }
                else if(numArr[i] <= 40){
                    area1[i].style.backgroundColor = "#aaa";
                }
                else if(numArr[i] <= 45) {
                    area1[i].style.backgroundColor = "#b0d840";
                }
            }
        }
    </script>
</body>
</html>
```

# 총평
## 부족한 점
![20201213_3](https://user-images.githubusercontent.com/70805241/102011342-cda53380-3d86-11eb-9d5b-c7cfc930ee78.JPG)<br>
위의 사진처럼 `+` 글자가 당첨 숫자를 누르기 전 초기 페이지에서 혼자 밑으로 내려와있다. 그런데 당첨숫자를 누르면 다른 영역들과 정렬이 맞아지는 기이한 현상.... 확실히 수업이 짧았던 HTML과 CSS 부분이 많이 약한 것 같다. 조금 더 공부해 본 다음에 수정을 해야할 것 같다. 아직까지 어떤 부분이 잘못됐는지 캐치조차 못하는 슬픈,,현실,,

