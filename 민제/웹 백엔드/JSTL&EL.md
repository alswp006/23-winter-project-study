# EL(Expression Language)

- 값을 표현하는데 사용하는 스크립트 언어로 JSP의 기본 문법을 보완

### 제공 기능

- JSP의 스코프(scope)에 맞는 속성 사용
- 집합 객체에 대한 접근 방법 제공
- 수치 연산, 관계 연산, 논리 연산자 제공
- 자바 클래스 메소드 호출 기능 제공
- 표현언어만의 기본 객체 제공

### 문법

```java
${expr}
// expr : 표현 언어가 정의한 문법에 따라 값을 표현하는 식

<b>${sessionScope.member.id}</b>
```

### 접근 규칙

- ${<표현 1>, <표현 2>}
    - 표현 1이나 표현 2가 null이면 null을 반환한다.
    - 표현1이 Map일 경우 표현2를 key로한 값을 반환한다.
    - 표현1이 List나 배열이면 표현2가 정수일 경우 해당 정수 번째 index에 해당하는 값을 반환한다.
        - 만약 정수가 아닐 경우에는 오류가 발생한다.
    - 표현1이 객체일 경우는 표현2에 해당하는 getter메소드에 해당하는 메소드를 호출한 결과를 반환한다.

### 예제

- 스코프 예제

```java
<%
    pageContext.setAttribute("p1", "page scope value");
    request.setAttribute("r1", "request scope value");
    session.setAttribute("s1", "session scope value");
    application.setAttribute("a1", "application scope value");
%>
<html>
<head>
    <title>Title</title>
</head>
<body>
pageContext.getAttribute("p1") : ${pageScope.p1 }<br>
request.getAttribute("r1") : ${requestScope.r1 }<br>
session.getAttribute("s1") : ${sessionScope.s1 }<br>
application.getAttribute("a1") : ${applicationScope.a1 }<br>
<br><br>
pageContext.getAttribute("p1") : ${p1 }<br>
request.getAttribute("r1") : ${r1 }<br>
session.getAttribute("s1") : ${s1 }<br>
application.getAttribute("a1") : ${a1 }<br>
</body>
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/e3f5402a-078e-431f-b27c-08e4f43fa913/Untitled.png)

- 사칙연산 예제

```java
<%
    request.setAttribute("k", 10);
    request.setAttribute("m", true);
%>
<html>
<head>
    <title>Title</title>
</head>
<body>
k : ${k } <br>
k + 5 : ${ k + 5 } <br>
k - 5 : ${ k - 5 } <br>
k * 5 : ${ k * 5 } <br>
k / 5 : ${ k div 5 } <br>

k : ${k }<br>
m : ${m }<br>
k > 5 : ${ k > 5 } <br>
k < 5 : ${ k < 5 } <br>
k <= 10 : ${ k <= 10} <br>
k >= 10 : ${ k >= 10 } <br>
m : ${ m } <br>
!m : ${ !m } <br>
</body>
</html>
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/c7754fad-cf55-40c2-98a6-cfc8878e60a6/Untitled.png)

- EL 문법 사용하지 않고 문자열 그대로 표시할 때

```markup
<%@ page isELIgnored = "true" %>
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/6a397b8b-c204-4cac-8c69-7f0d897e1edb/Untitled.png)

# JSTL(JSP Standard Tag Library)

- JSP 페이지에서 조건문 처리, 반복문 처리 등을 html tag 형태로 작성할 수 있다.
