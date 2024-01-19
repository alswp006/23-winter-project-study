# JSP
- 모든 jsp는 servlet으로 바뀌어서 동작한다.
    - “<%”, “%>” 과 같은 부분은 servlet으로 어떻게 바꿀지 알려주는 부분이다.
- “<%”, “%>”, “page”, “@”과 같은 부분을 지시자라고 한다.
- “<%=total%>”과 같은 것을 표현식이라 한다.

## J**SP의 실행순서**

1. 브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
2. 브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
3. 서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
4. 서블릿 클래스를 로딩하고 인스턴스를 생성한다.
5. 서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.

### sum10.jsp가 실행될 때 벌어지는 일

- 워크 스페이스 아래의 .metadata 폴더에 sum10_jsp.java 파일이 생성된다.
- 해당 파일의 _jspService() 메소드 안을 살펴 보면 jsp파일의 내용이 변환되서 들어가 있는 것을 확인할 . 수있다.
- sum10_jsp.java는 서블릿 소스로 자동으로 컴파일되고 실행되며 브라우저에 보여진다.

### _jspService

- jsp 파일에 어떤 코드를 썼던 간에 모든 코드는 jspService()라는 메소드 안으로 들어간다.
    
    → 응답에 포함되는건 service()밖에 없기 때문에
    
    - jsp에서 항상 service에밖에 못쓰는 것은 아님
        - <%! %> 에 메소드나 필드를 선언하면 이 메소드 바깥쪽에 해당 필드들이 만들어지도록 할 수 있다.

```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
hello~
<%
  System.out.println("jspService()");
%>

<%!
    public void  jspInit(){
        System.out.println("jspInit()");
    }
%>

<%!
    public void  jspDestroy(){
        System.out.println("jspDestroy()");
    }
%>
</body>
</html>
```

## JSP 문법

- JSP 페이지에서는 선언문(Declaration), 스크립트릿(Scriptlet), 표현식(Expression) 이라는 3가지의 스크립트 요소를 제공한다
- 선언문 - <%! %>
    - 전역 변수, 멤버 변수 선언 및 메소드 선언에 사용
    - service 메소드가 아닌 클래스 바디 쪽에 해당 코드 선언
- 스크립트릿 - <% %>
    - 프로그래밍 로직 기술에 사용
    - 일반적으로 가장 많이 사용
    - 모두 service()메소드 안에 선언됨
    - 예제
    
    ```java
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
    <%
        for (int i = 1; i <= 5; i++){
    %>
    <H<%=i%>>안녕하모니카</H<%=i%>>
    <%
        }
    %>
    </body>
    </html>
    ```
    
    <img width="667" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/f5625f1c-8fcd-4130-82cf-bc227053802b">
    
- 표현식 - <%=%>
    - 화면에 출력할 내용 기술에 사용
- 선언문, 표현식 예제
    
    ```java
    	<body>
    id : <%=getId() %> // 표현식
    <%! // 선언문
        String id = "10101"; // 멤버 변수 선언
        public String getId(){ // 메소드 선언
            return id;
        }
    %>
    </body>
    
    ```
    

## 주석

- JSP페이지에서는 HTML, JAVA, JSP의 주석을 모두 사용할 수 있다.

### HTML주석

- <!-- 주석 문장 -->의 형태
- HTML 주석은 HTML주석을 사용한 페이지를 웹에서 서비스할 때 화면에 주석이 내용이 표시되지는 않으나, [소스보기]수행하면 HTML주석의 내용이 화면에 표시.

### JSP주석

- JSP 페이지에서만 사용되며 <%-- 주석 문장 --%>의 형태
- JSP 주석은 해당 페이지를, 웹 브라우저를 통해 출력 결과로서 표시하거나, 웹 브라우저 상에서 소스 보기를 해도 표시 되지 않음. 또한 JSP주석 내에 실행코드를 넣어도 그 코드는 실행되지 않음.

### JAVA 주석

- //, /**/을 사용해서 작성.
- //은 한 줄짜리 주석을 작성할 때 사용되고, /**/은 여러 줄의 주석을 작성할 때 사용

→ 각각의 주석이 언제 주석의 역할을 하는지 잘 생각하여 사용

## JSP 내장 객체

- JSP의 코드는 대부분 서블릿 소스의 _jspService() 메소드 안에 삽입되는 코드로 생성된다.
- _jspService()에 삽입된 코드의 윗 부분에 미리 선언된 객체들이 있는데, 해당 객체들은 jsp에서도 사용 가능하다.
- response, request, application, session, out과 같은 변수들을 내장 객체라고 한다.
- 예시
    
    ```java
    <body>
    <%
        StringBuffer url = request.getRequestURL();
        out.println("url : " + url.toString());
    %>
    </body>
    ```
