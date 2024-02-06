# Spring Boot 프로젝트 환경설정

### 1. https://start.spring.io/ 사이트 접속

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/b8f5f386-ab5b-4a62-b15d-9fdfd2eabfd2/Untitled.png)

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

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/c96a628e-f088-414d-99c7-356361ea7bbb/Untitled.png)

> 오라클과 자바 라이센스 문제로 모든 `javax` 패키지를 `jakarta` 로 변경해줘야 한다.
> 

### 6. intellij - open project - 해당 폴더의 build.gradle Open

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/01390572-419c-408a-a293-98c55d261bf5/Untitled.png)

- .idea : intellij가 사용하는 설정 파일
- gradle : gradle을 사용하는 폴더
- build.gradle : 프로젝트를 설정하는 코드가 담긴 파일
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/038888dd-61ab-451e-9081-a9f126331cbd/Untitled.png)
    

### 7. main 파일을 실행시켜 서버가 정상 작동 하는지 확인해보기

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/389ea8f4-9139-4c87-aacc-0b09d7cf2258/Untitled.png)

- localhost:8080으로 접속

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/337218d7-ce3c-47b6-b585-f5cc062550b0/Untitled.png)

- 위와 같이 페이지가 뜨면 성공!
- @SpringBootApplication
    - Spring Boot 애플리케이션 실행
    - Tomcat이라는 웹서버를 내장하고 있어 Tomcat을 자체적으로 실행시킨다.

### 8. Gradle 실행을 Intellij IDEA 실행으로 변경

- Intellij IDEA - Setting -Build, Execution, Deployment - Gradle - Build and run using과 Run tests using을 IntelliJ IDEA로 변경

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0ee43fab-2947-49b1-b42b-cf1eb07e56bc/0bf00b11-85de-424e-9698-9e05567e9a27/Untitled.png)

- gradle 실행은 gradle을 통해 실행시켜서 느리다. 그러므로 Intellij IDEA 실행으로 변경해주어 Intellij에서 바로 실행시키도록 변경해준다.
