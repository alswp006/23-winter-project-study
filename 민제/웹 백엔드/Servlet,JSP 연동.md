- Servlet은 프로그램 로직이 수행되기에 유리하고 JSP는 결과를 출력하기에 유리하기 때문에 프로그램 로직 수행은 Servlet에서 결과 출력은 JSP에서 하는 것이 유리하다.
- 이러한 것은 이뤄주는 것이 Servlet에서 프로그램 로직을 수행하고 그 결과를 포워딩하여 JSP로 보내주는 방법이다. 이를 Servlet&JSP 연동이라고 한다.
- 예제
    - LogicServlet
    
    ```java
    @WebServlet("/LogicServlet")
    public class LogicServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;
    
        public LogicServlet() {
            super();
            // TODO Auto-generated constructor stub
        }
    
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            int v1 = (int)(Math.random() * 100) + 1;
            int v2 = (int)(Math.random() * 100) + 1;
            int result = v1 + v2;
    
            request.setAttribute("v1", v1);
            request.setAttribute("v2", v2);
            request.setAttribute("result", result);
    
            RequestDispatcher requestDispatcher = request.getRequestDispatcher("/result.jsp");
            requestDispatcher.forward(request, response);
        }
    
    }
    ```
    
    - result.jsp
    
    ```java
    <html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Insert title here</title>
    </head>
    <body>
    EL표기법으로 출력합니다.<br>
    ${v1} + ${v2} = ${result} <br><br>
    // 해당 변수값을 알아서 찾아옴
    // 최대한 자바 코드를 없애기 위한 노력
    
    스클립틀릿과 표현식을 이용해 출력합니다.<br>
    <%
        int v1 = (int)request.getAttribute("v1");
        int v2 = (int)request.getAttribute("v2");
        int result = (int)request.getAttribute("result");
    %>
    
    <%=v1%> + <%=v2 %> = <%=result %>
    </body>
    </html>
    ```
    
    <img width="666" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/ee61980f-059d-4974-9963-7dc40a9023f2">
    
- jsp에서는 되도록 자바 코드를 줄이는 것이 좋다. 이를 위해서 나온 것이 JSTL과 EL이다.
- 이는 추후 공부한다.
