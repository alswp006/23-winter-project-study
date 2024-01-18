# Servlet
- URL 요청을 처리하는 프로그램
- 자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할
- WAS에서 동작하는 Java 클래스
- HttpServlet클래스를 상속받아야함
- servlet과 JSP로부터 최상의 결과를 얻으려면 웹 페이지를 개발할 때 두 가지를 조화롭게 잘 사용하여야 한다.
    - ex) HTML은 JSP로 표현하고 복잡한 프로그래밍은 servlet으로 구현

## 자바 웹 어플리케이션

- WAS에 설치되어 동작하는 어플리케이션
- HTML, CSS, 이미지, 자바로 작성된 클래스(Servlet, package, interface 등), 각종 설정 파일 등이 포함됨

## Servlet 생명주기

- Servlet 생명주기를 확인할 수 있는 LifecycleServlet 클래스를 만들고 HttpServlet클래스의 init(), service(), destroy() 메소드를 오버라이드한다.
- 생성자와 각 메소드에 콘솔 출력으로 각 메소드가 언제 실행되는지 확인한다.

```java
@WebServlet("/LifecycleServlet")
public class LifecycleServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
 
    public LifecycleServlet() {
        System.out.println("LifecycleServlet 생성!!");
    }

	public void init(ServletConfig config) throws ServletException {
		System.out.println("init test 호출!!");
	}

	
	public void destroy() {
		System.out.println("destroy 호출!!");
	}

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
       {
		System.out.println("service호출!!");		
	}
	
}
출력
LifecycleServlet 생성!!
init test 호출!!
service호출!!
```

- 서블릿은 서버에 서블릿 객체를 여러 개 만들지 않는다. 요청이 올 때마다 객체를 생성하지 않고 한 번 생성되면 객체가 있는지 확인을 계속하며 사용한다.
- servlet의 생명 주기
    1. WAS는 서블릿 요청을 받으면 해당 서블릿이 메모리에 있는지 확인한다.
    2. 메모리에 없다면 해당 서블릿 클래스를 메모리에 올리고 init() 메소드를 실행한다.
    3. service() 메소드를 실행한다.
        1. WAS가 종료되거나, 웹 어플리케이션이 새롭게 갱신될 경우 destroy() 매소드가 실행된다.

### service()

- service()메소드를 오버라이드하지 않으면 부모 클래스인 HttpServlet의 service()메소드 실행
- HttpServlet의 service 메소드는 템플릿 메소드 패턴으로 구현
    - 클라이언트 요청이 GET일 때는 자신의 doGet(request, response) 메소드를 호출
    - 클라이언트 요청이 POST일 때는 자신의 doPost(request, response) 메소드를 호출
- 예제 코드

```java
package com.example.demo1;

import java.io.*;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.*;
import javax.servlet.annotation.*;

@WebServlet(name = "helloServlet", value = "/hello-servlet")
public class HelloServlet extends HttpServlet {

    public HelloServlet(){
        System.out.println("LifeCycle 생성");
    }

    public void init(ServletConfig config) throws ServletException {
        System.out.println("init test 호출!!");
    }

    public void destroy() {
        System.out.println("destroy 호출!!");
    }

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>form</title></head>");
        out.println("<body>");
        out.println("<form method='post' action='hello-servlet'>");
        out.println("name : <input type='text' name='name'><br>");
        out.println("<input type='submit' value='ok'><br>");
        out.println("</form>");
        out.println("</body>");
        out.println("</html>");
        out.close();
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        String name = request.getParameter("name");
        out.println("<h1> hello " + name + "</h1>");
        out.close();
    }
}
```

## **요청과 응답**

- 웹 브라우저에 URL을 입력하면 웹 브라우저는 도메인과 포트번호를 이용하여 서버에 접속함 그리고 클라이언트의 다양한 요청 정보를 서버에 전송한다.
- WAS는 웹 브라우저(클라이언트)로부터 Servlet요청을 받으면, 요청할 때 가지고 있는 정보를 HttpServletRequest객체를 생성하고 웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse객체를 생성한다.
- 생성된 HttpServletRequest(요청할 때 가지고 들어온 정보들), HttpServletResponse(클라이언트에게 전송하기 위한 정보들) 객체를 서블릿에게 전달한다.

### **HttpServletRequest**

- http프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용한다.
- 헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있다.
- Body의 Stream을 읽어 들이는 메소드를 가지고 있다.

### **HttpServletResponse**

- WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServleResponse객체를 생성하여 서블릿에게 전달한다.
- 서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메시지등을 전송한다.

→항상 응답으로 보내기 위한 부분은 response 객체에 담고 요청에 들어온 것들은 request에 담고있으니 내가 꺼내올 정보들은 request에서 꺼내온다.

### 헤더 정보 읽어들이기

- 웹 브라우저가 요청 정보를 담아서 보내는 header 값을 읽어들여 브라우저 화면에 출력한다.
- 실습코드
    
    ```java
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.util.Enumeration;
    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    
    @WebServlet("/header")
    public class HeaderServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;
    
        public HeaderServlet() {
            super();
            // TODO Auto-generated constructor stub
        }
    
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html>");
            out.println("<head><title>form</title></head>");
            out.println("<body>");
    
            Enumeration<String> headerNames = request.getHeaderNames();
            while(headerNames.hasMoreElements()) {
                String headerName = headerNames.nextElement();
                String headerValue = request.getHeader(headerName);
                out.println(headerName + " : " + headerValue + " <br> ");
            }
    
            out.println("</body>");
            out.println("</html>");
        }
    
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            doGet(request, response);
        }
    }
    ```
    

### 파라미터 읽어들이기

- URL주소의 파라미터 정보를 읽어 들여 화면에 출력해보기
- URL주소의 ‘?’뒤가 파라미터
- 실습 코드
    
    ```java
    import java.io.IOException;
    import java.io.PrintWriter;
    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    
    @WebServlet("/param")
    public class ParameterServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;
    
        public ParameterServlet() {
            super();
            // TODO Auto-generated constructor stub
        }
    
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html>");
            out.println("<head><title>form</title></head>");
            out.println("<body>");
    
            String name = request.getParameter("name");
            String age = request.getParameter("age");
    
            out.println("name : " + name + "<br>");
            out.println("age : " +age + "<br>");
    
            out.println("</body>");
            out.println("</html>");
        }
    }
    ```
    
    <img width="673" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/fb605fc2-6b7a-40e0-bffe-4b7694714fe1">
    
    - 현재는 name과 age가 null이다. URL에서 ‘?’뒤에 파라미터 값을 넣어주면 값이 생성된다.
    
    <img width="669" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/4074e407-e3e8-4576-b695-b1ad48a6b676">
    
    ⇒ 동적인 페이지
    
    - 이러한 파라미터는 URL에서만 넘어오는 것뿐만 아니라 HTML의 form 태그 안의 input 태그의 값들도 파라미터로 넘어온다.

### 그 외의 요청정보 출력

```java
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/info")
public class InfoServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public InfoServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>info</title></head>");
        out.println("<body>");

        String uri = request.getRequestURI();
        StringBuffer url = request.getRequestURL();
        String contentPath = request.getContextPath();
        String remoteAddr = request.getRemoteAddr();

        out.println("uri : " + uri + "<br>");
        out.println("url : " + url + "<br>");
        out.println("contentPath : " + contentPath + "<br>");
        out.println("remoteAddr : " + remoteAddr + "<br>");

        out.println("</body>");
        out.println("</html>");
    }
}
```

<img width="697" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/fa7c6906-a83b-42bd-a981-a3af4fee2fb5">

> URI : 포트번호 이하부분이 나오는것이다.
> URL: 요청 주소 전체
