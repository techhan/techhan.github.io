---
title:  "JSP 내장 객체"
excerpt: "JSP 기본"
categories: 
  - Study
tags: 
  - JSP
toc : true
---


## JSP 내장 객체란?
> JSP 내장객체란 'JSP 내에서 선언하지 않고 사용할 수 있는 객체' 라는 의미에서 붙여진 이름이다. <br>
구조적으로는 JSP가 서블릿 형태로 자동 변환된 코드 내에 포함되어 있는 `멤버 변수`, `메서드 매개변수` 등의 각종 `참조 변수(객체)`를 말한다. <br>
서블릿 컨테이너가 해당 JSP 페이지 실행 시 자동으로 생성한다. JSP가 변환된 jsp.java 파일을 열어보면 _jspService() 메서드 내부에 선언되어 있다.
<br>


<br><br>


## JSP 내장 객체 종류


|내장 객체|반환값 타입|설명|
|:------:|:------:|:--------:|
|request|javax.servlet.http.httpServletRequest <br> 또는 javax.servlet.ServeltRequest|웹 브라우저의 요청 정보를 저장하고 있는 객체|
|response|javax.servlet.http.httpServletResponse <br> 또는 javax.servlet.ServletResponse|웹 브라우저의 요청에 대한 응답 정보를 저장하는 객체|
|out|javax.servlet.jsp.JspWriter|JSP 페이지의 출력할 내용을 가지고 있는 출력 스트림 객체|
|session|javax.servlet.http.HttpSession|하나의 웹 브라우저 내에서 정보를 유지하기 위한 세션 정보를 저장하고 있는 객체|
|application|javax.servlet.ServletContext|웹 애플리케이션 Context의 정보를 담고 있는 객체|
|pageContext|javax.servlet.jsp.PageContext|JSP 페이지에 대한 정보를 저장하고 있는 객체|
|page|java.lang.Object|JSP 페이지를 구현한 자바 클래스 객체|
|config|javax.servlet.ServletConfig|JSP 페이지에 대한 설정 정보를 담고 있는 객체|
|exception|java.lang.Throwable|JSP 페이지에서 예외가 발생한 경우 사용하는 객체|

<br><br>

## 내장 객체 영역
> 웹 애플리케이션은 page, request, session, application 4개의 영역(scope)을 가진다. 내장 객체의 영역은 `객체의 유효기간`이라고도 불리며 객체를 누구와 공유할 것인가를 의미한다.


<br><br>

### page 영역
- 한 번의 웹 브라우저(클라이언트)의 요청에 대해 하나의 JSP가 호출된다.
- page 영역은 객체를 하나의 페이지 내에서만 공유한다.
- pageContext 내장 객체를 사용한다.


<br>

### request 영역
- 한 번의 웹 브라우저의 요청에 대해 같은 요청을 공유하는 페이지가 대응된다.
- 같은 request 영역인 경우 두 개의 페이지가 같은 요청을 공유할 수 있다.
- 객체를 하나 또는 두 개의 페이지 내에서 공유가 가능하다.
- include, forward 액션 태그 사용시 request 내장 객체를 공유하게 되며 그에 따라 같은 request 영역이 된다.
- request 내장 객체를 사용한다.

<br>

### session 영역
- 하나의 웹 브라우저당 1개의 session 객체 생성한다.
- 같은 웹 브라우저 내에서 요청되는 페이지들은 같은 객체를 공유한다.
- 주로 회원 관리(인증)에 사용되며 session 내장 객체를 사용한다.

<br>

### application 영역
- 하나의 웹 애플리케이션(프로젝트)당 1개의 application 객체를 생성한다.
- 같은 웹 애플리케이션에 요청되는 페이지들은 같은 객체를 공유한다.
- 애플리케이션 전체에서 공유하는 객체이므로 메모리에 부담이 갈 수 있어서 자주 사용되진 않는다.
- application 내장 객체를 사용한다.