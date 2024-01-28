# API(Application Programming Interface)

- 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스
- 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스 제공

## REST API(REpresentational State Transfer API)

- REST형식의 API
- 핵심 컨텐츠 및 기능을 외부 사이트에서 활용할 수 있도록 제공되는 인터페이스

### REST API의 제약 조건

- client-server
- stateless
- cache
- uniform interface
- layered system
- code-on-demand (optional)
- HTTP 프로토콜을 사용한다면 uniform interface을 제외한 제약 조건은 지킬 수 있다.
- uniform interface
    - 리소스가 URI로 식별되야 한다.
    - 리소스를 생성,수정,추가하고자 할 때 HTTP메시지에 표현을 해서 전송해야 한다.
    - 메시지는 스스로 설명할 수 있어야 한다. (Self-descriptive message)
    - 애플리케이션의 상태는 Hyperlink를 이용해 전이되야 한다.(HATEOAS)
- 메시지가 스스로 설명할 수 있어야 하는 부분과 HATEOAS를 지원하는 것은 API로 쉽지 않다.

## WEB API(혹은 HTTP API)

- REST API는 uniform interface를 지원하는 것이 쉽지 않기 때문에 많은 서비스가 REST에서 바라는 것을 모두 지원하지 않고 API를 만든다.
- REST의 모든 것을 제공하지 않으면서 REST API라고 말하는 경우가 있고 Web API 혹은 HTTP API라고 부르는 경우가 있다.
- WEB API 디자인 가이드
    - URI는 정보의 자원을 표현해야하며 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

### HTTP Method

- POST : 해당 URI를 요청하면 리소스를 생성한다.
- GET : 해당 리소스를 조회한다. 리소스를 조회하고 해당 document에 대한 자세한 정보를 가져온다.
- PUT : 해당 리소스를 수정한다.
- DELETE : 해당 리소스를 삭제한다.

### URI

- **슬래시 구분자(/)는 계층을 나타낼 때 사용**
- http://domain/houses/apartments
- http://domain/departments/1/employees
    - URI 마지막 문자로 슬래시 구분자(/)를 포함하지 않는다.
    - 하이픈(-)은 URI가독성을 높일 때 사용한다.
    - 언더바(_)는 사용하지 않는다.
    - URI경로는 소문자만 사용한다.
    - RFC 3986(URI 문법 형식)은 URI스키마와 호스트를 제외하고는 대소문자를 구별한다.
    - 파일 확장자는 URI에 포함하지 않는다.
    - Accept Header를 사용한다.

### 상태 코드(성공)

- 200 : 클라이언트 요청 정상 수행
- 201 : 클라이언트가 요청한 리소스 생성이 성공적으로 수행(POST를 통한 리소스 생성 작업 시)

### 상태 코드(클라이언트로 인한 오류)

- 400 : 클라이언트 요청이 부적절
- 401 : 미인증된 클라이언트가 보호된 리소스를 요청 (로그인하지 않은 유저가 로그인했을 때 요청가능한 리소스를 요청했을 때)
- 403 : 유저 인증 상태와 관계없이 응답하고 싶지 않은 리소스를 요청(403보다는 400, 404 사용을 권고)
- 405 : 클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우(doGet메소드만 가지고있는데 사용자가 POST를 요청했을 때)

### 상태 코드(서버로 인한 오류)

- 301 : 클라이언트가 요청한 리소스에 대한 URI가 변경되었을 때 (응답 시 Location Header에 변경된 URI를 적어줘야 함)
- 500 : 서버에 문제가 있을 때

## WEB API 실습

### 데이터베이스의 전체 데이터를 json 형태로 가져와 출력하기

- EmplServlet.java

```java
@WebServlet("/empl")
public class EmplServlet extends HttpServlet{
    public EmplServlet(){
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setCharacterEncoding("utf-8");
        response.setContentType("application/json");

        EmployeeDao dao = new EmployeeDao();

        List<Employee> list = dao.getEmployees();

        ObjectMapper objectMapper = new ObjectMapper();
        String json = objectMapper.writeValueAsString(list);

        PrintWriter out = response.getWriter();
        out.println(json);
        out.close();
    }
}
```

- 출력 결과

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/0d8a6fd0-25e0-4078-999d-3f5679fabc18/Untitled.png)
