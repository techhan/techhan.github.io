---
title:  "[github pages] minimal mistakes 사이드 바 카테고리 정렬"
excerpt: "카테고리 정렬, 포스트 왼쪽에 카테고리 추가하기"

categories: 
  - etc
tags: 
  - jekyll
  - blog
---

## 문제
![기존카테고리](https://user-images.githubusercontent.com/70805241/113517671-653fc380-95bc-11eb-838e-ab11fcd569b0.png) <br><br>
위의 사진처럼 `etc(1)`가 제일 상단에 있어 눈에 거슬렸다. 이것저것 찾아보면서 파일들을 건드려봤더니 `_includes > nav_list_main` 파일이 카테고리와 관련된 걸 알 수 있었다.


### 기존 코드
![기존코드](https://user-images.githubusercontent.com/70805241/113518401-12b4d600-95c1-11eb-9820-3dfda2f9a0b4.png)


카테고리 정렬과 직접적인 관련이 있는 코드는 v-show="flag_c"가 적힌 ul 태그 바로 하단 코드였다. for문은 뭔가 어려워 보이지만 자바스크립트 for in과 사용법이 비슷해 보인다. category[0]은 category name, {{category[1].size}} 이 부분은 카테고리 내 포스트 개수를 의미한다.


### 변경된 코드
![추가코드](https://user-images.githubusercontent.com/70805241/113518466-7dfea800-95c1-11eb-84da-f175dc89f3fb.png)

`assing` 태그는 새로운 Liquid 변수를 생성한다. 8번 코드는 sorted_categories라는 변수를 생성하고 site.categories(전체 카테고리)를 정렬(sort)해서 담는다. 알파벳순으로 정렬된 sorted_categories를 category 변수로 하나씩 꺼내는 형태이다.


## 결과
![변경된카테고리](https://user-images.githubusercontent.com/70805241/113518604-50662e80-95c2-11eb-9310-b63748079bb4.png)  ![루피](https://user-images.githubusercontent.com/70805241/113518653-9e7b3200-95c2-11eb-9f1a-b7184fb17830.png)

<br>

-------------------------------


## 문제
![포스팅사이드문제](https://user-images.githubusercontent.com/70805241/113518705-f5810700-95c2-11eb-9fff-a34242d8589d.png) 

카테고리 정렬을 성공적으로 마친 후 TIL 카테고리에 테스트 포스팅을 해봤는데 왼쪽 사이드 바 메뉴 부분에 저렇게 영어로 떡하니 Category가 생겨서 일단 vs 코드에서 Category를 검색했다. 범인은 바로 `_config.yml`였다.

```
- scope:
    path: "_posts/TIL"
    type: posts
values:
    layout: single
    classes: wide
    author_profile: true
    comments: true
    share: true
    search: true
    related: true
    sidebar:
        title : Category
        nav: sidebar
```


## 해결

관련 없는 코드를 싹 지우고 하단 코드만 남겨두었다.

```
# _posts
- scope:
    path: ""
    type: posts
values:
    layout: single
    classes: wide
    author_profile: true
    comments: true
    share: true
    search: true
    related: true
```

<br>

변경하고 보니 원래부터 게시글 페이지 좌측에 카테고리 표시를 나타내고 싶었는데 일단 그 부분에 이상하지만 뭔가 나타나서 조금 더 파일들을 만져보기로 했다. 잘 모르겠지만 일단 위의 코드에 sidebar 부분 추가!

```
# _posts
- scope:
    path: ""
    type: posts
values:
    layout: single
    classes: wide
    author_profile: true
    comments: true
    share: true
    search: true
    related: true
    sidebar:
        nav: sidebar
```

<br>

그리고 vs 코드에서 `sidebar`를 검색해봤다. 여러 파일들을 봤는데 이 코드가 제일 연관 있는 것 같았다. <br>

![side코드](https://user-images.githubusercontent.com/70805241/113519028-cc617600-95c4-11eb-8daf-0c2ff4ab35ff.png) <br>


후다닥 `_includes > nav_list` 파일을 `nav_list_main` 내용을 복사해 붙여넣었다.


## 결과

![사이드바카테고리](https://user-images.githubusercontent.com/70805241/113519111-2a8e5900-95c5-11eb-8e17-cd90a027fe06.png)

![루피](https://user-images.githubusercontent.com/70805241/113518653-9e7b3200-95c2-11eb-9f1a-b7184fb17830.png)


<br><br>

----------------------

### 참고
- [카테고리 정렬 참고 블로그](https://eastglow.github.io/%EA%B8%B0%ED%83%80/2018/07/05/Jekyll-posts-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%9D%98-categories-%EC%A0%95%EB%A0%AC-%EC%88%9C%EC%84%9C-%EB%B0%94%EA%BE%B8%EA%B8%B0.html)