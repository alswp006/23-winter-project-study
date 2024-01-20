# redirect

- redirect는 Http프로토콜로 정해진 규칙으로 서버가 클라이언트로부터 요청을 받은 후, 클라이언트에게 특정 URL로 이동하라고 요청하는 것을 의미한다.
- 서버는 클라이언트에게 HTTP 상태코드 302로 응답하는데 이때 헤더 내 Location 값에 이동할 URL 을 추가한다. 클라이언트는 리다이렉션 응답을 받게 되면 헤더(Location)에 포함된 URL로 재요청을 보내게 된다. 이때 브라우저의 주소창은 새 URL로 바뀌게 된다..
- 클라이언트는 서버로부터 받은 상태 값이 302이면 Location헤더값으로 재요청을 보내게 된다. 이때 브라우저의 주소창은 전송받은 URL로 바뀌게 된다.
- 서블릿이나 JSP는 리다이렉트하기 위해 HttpServletResponse 클래스의 sendRedirect() 메소드를 사용한다.
- 예제
    
    ```java
    <body>
    <%
        response.sendRedirect("index.jsp");
    %>
    </body>
    ```
    
    <img width="666" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/a33e79f2-3b1c-4675-88bf-e9bba3c18a5d">
    

## **브라우저에서 리다이렉트 확인**

- 크롬에서 우측버튼을 누르고 검사를 선택한 후 Network탭을 선택한다.
- redirect01.jsp를 실행하면 서버로부터 응답코드로 302를 받는 것을 알 수 있다.

<img width="669" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/745950f7-ebc3-41fc-885e-3f4f6ea86c14">

# forward

1. 웹 브라우저에서 Servlet1에게 요청을 보냄
2. Servlet1은 요청을 처리한 후, 그 결과를 HttpServletRequest에 저장
3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송(forward)
4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청을 처리한 후 웹 브라우저에게 결과를 전송
- 클라이언트는 Servlet1에만 요청을 주고 Servlet1이 forward를 통해 다른 Servlet에게 맡겨서 요청을 처리하는지 혼자 처리하는지 알 필요가 없기 때문에 forward가 실행되고 나서는 URL이 바뀌지 않는다.
    - 실제 클라이언트가 서버에 요청하면 request, response라는 것들이 반드시 생성되었는데 forward 작업을 해도 request, response는 계속 유지되어 있다. 하지만 redirect 작업에서는 요청이 여러 번 왔다갔다하며 모두 서로 다른 요청이다.
    
    **→ forward와 redirect의 가장 큰 차이점은 요청이 하나인지 여러개인지이다.**
    
- 예제
    - front
    
    ```java
    @WebServlet("/front")
    public class FrontServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;
    
        public FrontServlet() {
            super();
        }
    
        protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            int diceValue = (int)(Math.random() * 6) + 1;
            request.setAttribute("dice", diceValue);
            // 파라미터 1 : 식별할 수 있는 값(id), 파라미터 2 : 가지는 값(value)
    
            RequestDispatcher requestDispatehcer = request.getRequestDispatcher("/next");
            // 어디로 이동할것인지 RequestDispatcher로 얻는다. (/로 시작, 컨텐츠 루트 이하로, 같은 어플 내에서 이동 가능)
            requestDispatehcer.forward(request, response);
            //인자로 request, response 전달
        }
    
    }
    ```
    
    - next
    
    ```java
    @WebServlet("/next")
    public class NextServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;
    
        public NextServlet() {
            super();
            // TODO Auto-generated constructor stub
        }
    
        protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html>");
            out.println("<head><title>form</title></head>");
            out.println("<body>");
    
            int dice = (Integer)request.getAttribute("dice");
            out.println("dice : " + dice);
            for(int i = 0; i < dice; i++) {
                out.print("<br>hello");
            }
            out.println("</body>");
            out.println("</html>");
        }
    
    }
    ```
    
    <img width="666" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/8c74bd8c-471c-4374-aff5-50346dce12e8">
    
    → URL 변화 없음
