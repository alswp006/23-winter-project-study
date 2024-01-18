## 구현 코드

- MainServlet.java

```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet(name = "main", value = "/main")
public class MainServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public MainServlet(){
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        out.println("<head><title>main</title></head>");
        out.println("<a href=\"time\">time<a/>");
    }
}
```

- TimeServlet.java

```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

@WebServlet(name = "time", value = "/time")
public class TimeServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public TimeServlet(){
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        PrintWriter out = response.getWriter();

        LocalDateTime now = LocalDateTime.now();
        String time = now.format(DateTimeFormatter.ofPattern("yyyy/MM/dd HH:mm"));
        out.println("<a href=\"main\">main<a/>");
        out.println("<h1>현재 시간 : " + time);
        out.println("<h1/>");
    }
}
```

- index.jsp

```java
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html>
<head>
    <title>JSP - Hello World</title>
</head>
<body>
</h1>
<br><a href="main">main</a>
</body>
</html>
```

<img width="317" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/38439bd1-c69f-4f4e-b862-2099c02f65ca">
<img width="425" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/cc974440-4d3a-4f9e-ba49-db45035581be">

