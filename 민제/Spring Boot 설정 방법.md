# Spring Boot 프로젝트 환경설정

> 스프링 부트에 대해 찾고 싶은 내용이 있을 때는 공식 문서 찾아보기
[Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
> 

## 프로젝트 생성

### 1. https://start.spring.io/ 사이트 접속

![](https://velog.velcdn.com/images/alswp006/post/1df3d83d-f9a4-4d2a-a85b-d82d3d6dec7f/image.png)

### 2. Project, Spring Boot 버전, Language, Packaging, java 버전 설정

- Project: **Gradle - Groovy** Project
- Spring Boot: **3.x.x**
- Language: Java
- Packaging: Jar
- Java: 17 또는 21

> 요즘은 maven보다는 gradle을 사용하는 추세이니 gradle로 project를 설정하자!
> 

> SNAPSHOT, M1는 베타 버전 등 공식적으로 나오지 않은 버전들을 의미한다.
> 

### 3. 프로젝트 Name과 Artifact 설정

- Artifact : 프로젝트가 빌드되어 나올 때 결과물의 이름

### 4. Dependency 추가

- Spring Web : web 프로젝트를 생성할 때 사용
- thymeleaf : html을 만들어주는 템플릿 엔진

### 5. GENERATE

![](https://velog.velcdn.com/images/alswp006/post/0b9371d6-2aba-4357-a1dc-d74d672904f5/image.png)


> 오라클과 자바 라이센스 문제로 모든 `javax` 패키지를 `jakarta` 로 변경해줘야 한다.
> 

### 6. intellij - open project - 해당 폴더의 build.gradle Open

![](https://velog.velcdn.com/images/alswp006/post/0968194f-1598-43f2-a957-be9dbb12687a/image.png)


- .idea : intellij가 사용하는 설정 파일
- gradle : gradle을 사용하는 폴더
- build.gradle : 프로젝트를 설정하는 코드가 담긴 파일
    
![](https://velog.velcdn.com/images/alswp006/post/43fdc31b-d0fc-46c3-ba49-5a27b3862990/image.png)

    

### 7. main 파일을 실행시켜 서버가 정상 작동 하는지 확인해보기

![](https://velog.velcdn.com/images/alswp006/post/d87100f6-2cce-420d-95ce-95d95cd775f7/image.png)


- localhost:8080으로 접속
![](https://velog.velcdn.com/images/alswp006/post/f10c0f7d-a249-40c8-a959-352b24892f53/image.png)


- 위와 같이 페이지가 뜨면 성공!
- @SpringBootApplication
    - Spring Boot 애플리케이션 실행
    - Tomcat이라는 웹서버를 내장하고 있어 Tomcat을 자체적으로 실행시킨다.

### 8. Gradle 실행을 Intellij IDEA 실행으로 변경

- Intellij IDEA - Setting -Build, Execution, Deployment - Gradle - Build and run using과 Run tests using을 IntelliJ IDEA로 변경

![](https://velog.velcdn.com/images/alswp006/post/fe95bca8-adcd-4dc3-8abc-83714e814c08/image.png)


- gradle 실행은 gradle을 통해 실행시켜서 느리다. 그러므로 Intellij IDEA 실행으로 변경해주어 Intellij에서 바로 실행시키도록 변경해준다.

## 프로젝트 파일

### dependency

- 프로젝트의 build.gradle을 보면 의존 관계는 `spring-boot-starter-thymeleaf`, `spring-boot-starter-web` 밖에 없는데 External Library에는 수많은 관련 Library들이 설치되어 있는 것을 확인해볼 수 있다.

![](https://velog.velcdn.com/images/alswp006/post/7647cc39-6b39-4c95-9aaa-937d1aaf1a5d/image.png)


- 이는 `spring-boot-starter-thymeleaf`, `spring-boot-starter-web`과 의존 관계가 있는 Library들이며 core, tomcat 등이 있는 것을 확인해볼 수 있다.

![](https://velog.velcdn.com/images/alswp006/post/cd47fb16-fa52-4eeb-8245-67dc138b9bc4/image.png)


- 또한 우측의 Gradle을 열어보면 `dependencies`들이 설치되어있는 것을 확인할 수 있다

![](https://velog.velcdn.com/images/alswp006/post/741b3458-0d94-4734-bd0c-41bf2a8fb897/image.png)

### tomcat

- 예전에는 Web Server를 이용하기 위해 Tomcat을 설치하고 거기에 java 코드를 밀어넣는 식으로 사용하였다.
- 하지만 현재는 프로젝트의 소스 라이브러리들이 웹서버를 내장하고 있기 때문에 Tomcat을 따로 설치하거나 따로 설정할 필요없이 웹서버를 사용할 수 있다.

## View 설정

- src - main - resources - static : 정적 페이지
    - static 폴더에 index.html 파일을 만들고 html 코드 작성
    
    ```java
    <!DOCTYPE HTML>
    <html xmlns:th="http://www.thymeleaf.org">
    <head>
      <title>Hello</title>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    </head>
    <body>
    Hello World!!
    </body>
    </html>
    ```
    
    - [localhost:8080](http://localhost:8080) 접속
    ![](https://velog.velcdn.com/images/alswp006/post/9795a98d-22b7-44d8-ab3d-6fd10de0432a/image.png)


    
- controller와 templetes - html 파일을 이용하여 실습해보기
    - java 패키지의 하위 패키지에 controller 패키지를 생성하고 [HelloController.java](http://HelloController.java) 파일 생성
    
    ```java
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class HelloController {
    
        //hello라는 이름의 Get으로 Mapping
        @GetMapping("hello")
        public String Hello(Model model){
            //data라는 이름으로 Hello World!!! 저장 Map의 key, value같은 느낌
            model.addAttribute("data", "Hello World!!!");
    
            //hello.html 파일을 찾아 랜더링
            return "hello";
        }
    }
    ```
    
    - resources - templetes 패키지에 hello.html 파일 생성
    
    ```java
    <!DOCTYPE HTML>
    <html xmlns:th="http://www.thymeleaf.org">
    <head>
      <title>Hello</title>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    </head>
    <body>
    <!--model에서 key 값이 data인 value를 찾아 대입-->
    <p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
    </body>
    </html>
    ```
    
    - 실행 후 [localhost:8080/hello로](http://localhost:8080/hello로) 접속
    ![](https://velog.velcdn.com/images/alswp006/post/6ac8db21-3dbc-4d8f-9e87-e64cdfa792e9/image.png)

    

## 실행 파일 만들기

1. 터미널 실행하여 프로젝트 디렉토리로 이동
![](https://velog.velcdn.com/images/alswp006/post/61cf1d8c-be53-44d6-981a-7bbe5d7043b1/image.png)

2. ./gradlew build 입력 후 build - libs 디렉토리로 이동
![](https://velog.velcdn.com/images/alswp006/post/deb26f74-e5c3-4006-beff-78e023403257/image.png)
- jar파일이 생성된 것을 확인할 수 있다.

3. java -jar jar파일의 이름을 입력하여 실행하여 준다.
![](https://velog.velcdn.com/images/alswp006/post/5ef1f341-aa6e-40ae-99dc-61138c290c76/image.png)

4. 실행 확인
![](https://velog.velcdn.com/images/alswp006/post/e4a40ded-7ace-4c2e-a600-d6b9eb7bdc8f/image.png)


> 스프링 부트에 대해 찾고 싶은 내용이 있을 때는 공식 문서 찾아보기
[Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
>
