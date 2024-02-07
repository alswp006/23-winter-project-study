# Spring MVC(Model-View-Controller)

- Model : 모델은 뷰가 렌더링하는데 필요한 데이터이다. 예를 들어 사용자가 요청한 상품 목록이나, 주문 내역이 이에 해당한다.
- View : 웹 애플리케이션에서 뷰(View)는 실제로 보이는 부분이며, 모델을 사용해 렌더링을 한다. 뷰는 JSP, JSF, PDF, XML등으로 결과를 표현한다.
- Controller : 컨트롤러는 사용자의 액션에 응답하는 컴포넌트이다. 컨트롤러는 모델을 업데이트하고, 다른 액션을 수행한다.

## MVC와 템플릿 엔진 연습

- controller와 view를 가지고 연습을 해보자!

### Controller

- HelloController

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {

		//hello-mvc라는 이름의 Get으로 Mapping
    @GetMapping("hello-mvc")
    //name이라는 이름으로 parameter를 받아 인자로 전달해준다.
    public String helloMvc(@RequestParam("name") String name, Model model) {
        //model에 name이라는 이름으로 전달
        model.addAttribute("name", name);

        //hello-templete.html 파일을 찾아 랜더링 (thymeleaf 템플릿 엔진 처리)
        return "hello-templete";
    }
}
```

### View

- hello-templete.html

```java
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```

### 실행
<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/82d1e57c-abfb-47ea-a5e3-05f120c12334">

- url뒤에 ?name=”내용”으로 내용 전달

## API 사용

### @ResponseBody를 사용하여 직접 html만들어 넘겨주기

```java
@Controller
public class HelloController {

    @GetMapping("hello-string")
    //html의 body부분에 내용을 직접 넘겨주겠다. html이 자동으로 생성되어 실행됨
    @ResponseBody
    public String helloString(@RequestParam("name") String name){

        return "hello, " + name;
    }
}
```

- 실행 결과
<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/fc173c36-0243-486b-8f84-5be18e94666c">


- 페이지 소스 보기로 확인
<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/553275f4-3c74-4be1-b5fa-5c585f3c999b">


<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/ffdf490c-c520-4720-90cb-ff61780b838a">

- 이 방법은 자주 사용되지 않는다

### json 방식

- json 찾아보기

```java
@Controller
public class HelloController {

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello {
        private String name;
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
    }
}
```

- 실행 결과
<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/1a19a126-cb6f-44be-a775-4a4aa2824bd5">


### @ResponceBody

- HTTP의 BODY에 문자 내용을 직접 반환
- `viewResolver` 대신에 `HttpMessageConverter` 가 동작
- 기본 문자처리: `StringHttpMessageConverter`
- 기본 객체처리: `MappingJackson2HttpMessageConverter`
- byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음

## Swagger

[https://velog.io/@borab/Spring-boot-Swagger-설정-gradle](https://velog.io/@borab/Spring-boot-Swagger-%EC%84%A4%EC%A0%95-gradle)

## lombok

https://devgoat.tistory.com/14

## **DispatcherServlet**

- 프론트 컨트롤러 (Front Controller)
- 클라이언트의 모든 요청을 받은 후 이를 처리할 핸들러에게 넘기고 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여준다.
- DispathcerServlet은 여러 컴포넌트를 이용해 작업을 처리한다.
<img width="707" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/9e398cd7-be80-40a6-a7d7-5a616c1a2d3f">

### 아티팩트 생성

https://getinfo.tistory.com/2
