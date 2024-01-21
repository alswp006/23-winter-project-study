# Scope

<img width="683" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/94d2e7a7-607b-4694-8e6c-497afd40316b">

### Application

- 웹 어플리케이션(프로젝트)이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
    - 하나의 서버에는 웹 어플리케이션이 여러 개 존재 가능
- ServletContext 인터페이스를 구현한 객체를 사용
- jsp에서는 application 내장 변수, servlet에서는 getServletContext()메소드를 이용하여 application 객체를 이용한다.
- 웹 어플리케이션 하나 당 하나의 application 객체가 사용된다.
- 모든 클라이언트가 공통적으로 사용해야할 값이 있을 때 사용한다.

### Session

- 웹 브라우저 별로 변수가 관리되는 경우 사용
- 여러 개의 요청이 들어와도 유지
- 웹 브라우저의 탭 간에는 세션 정보가 공유되기 때문에 각각의 탭에서 같은 세션 정보를 사용할 수 있다.
    - ex) 하나의 탭에서 로그인하면 다른 탭에서도 자동으로 로그인 되어 있음
- HttpSession 인터페이스를 구현한 객체를 사용한다.
- JSP에서는 session 내장 변수, Servlet에서는 HttpServletRequest를 사용한다.
- **장바구니처럼 사용자마다 유지되어야할 정보가 있을 때 사용된다.(각 클라이언트마다 정보 유지)**

### Request

- http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용
- 하나의 요청과 응답 (응답이 나갈 때 사라짐)
- 서블릿에서는 HttpServletRequest 객체, jsp에서는 request 내장 변수 사용
- 값 저장 : setAttribute(), 값 읽기 : getAttribute() 메소드 사용
- **forward시 값을 유지하고자 사용**

### Page

- 페이지 내에서 지역변수처럼 사용
- PageContext 추상 클래스를 사용하며 JSP에서 pageContext라는 내장 객체로 사용 가능하다.
- forward가 될 경우 해당 Page Scope에서 생성된 변수는 사용할 수 없다.
- jsp에서 Page Scope에 값을 저장한 후 해당 값을 EL 표기법 등에서 사용할 때나 지역변수처럼 해당 jsp나 servlet이 실행되는 동안만 유지시키고 싶을 때 사용한다.
- **지역 변수처럼 사용된다**

→ 네 스코프 모두 값 저장에 setAttribute, 값 읽기에 getAttrubute를 사용한다.

### ApplicationScope 예제

- ApplicationScope01.java

```java
@WebServlet("/ApplicationScope01")
public class ApplicationScope01 extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public ApplicationScope01() {
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        PrintWriter out = response.getWriter();
        ServletContext application = getServletContext();
        int value = 1;
        application.setAttribute("value", value);
        out.println("<h1>value : " + value + "</h1>");
    }
}
```

- ApplicationScope02.java

```java
@WebServlet("/ApplicationScope02")
public class ApplicationScope02 extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public ApplicationScope02() {
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        PrintWriter out = response.getWriter();
        ServletContext application = getServletContext();

        try {
            int value = (int)application.getAttribute("value");
            value++;
            application.setAttribute("value", value);
            out.println("<h1>value : " + value + "</h1>");
        }catch(NullPointerException ex) {
            out.println("value가 설정되지 않습니다.");
        }
    }
}
```

- applicationscope.jsp

```java
<body>
<%
    try{
        int value = (int)application.getAttribute("value");
        value = value + 2;
        application.setAttribute("value", value);
%>
<h1><%=value %></h1>
<%
}catch(NullPointerException ex){
%>
<h1>설정된 값이 없습니다.</h1>
<%
    }
%>
</body>
```

- 웹 어플리케이션이 다시 시작할 때까지 값이 유지된다.
