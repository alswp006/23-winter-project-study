# Spring JDBC

- JDBC 프로그래밍의 반복되는 저수준 세부사항을 스프링 프레임워크가 처리해준다.

## Spring JDBC 패키지

**org.springframework.jdbc.core**

- JdbcTemplate 및 관련 Helper 객체 제공
- JdbcTemplate
    - 리소스 생성, 해지를 처리하여 연결을 닫지않아 발생하는 문제를 예방한다.
    - Statement의 생성과 실행을 처리한다.
    - SQL조회, 업데이트, 저장 프로시저 호출, ResultSET 반복 호출 등을 실행한다.
    - JDBC예외 발생 시 일반적인 예외로 변환한다.

**org.springframework.jdbc.datasource**

- DataSource를 쉽게 접근하기 위한 유틸 클래스, 트랜젝션매니져 및 다양한 DataSource 구현을 제공

**org.springframework.jdbc.object**

- RDBMS 조회, 갱신, 저장등을 안전하고 재사용 가능한 객제 제공

**org.springframework.jdbc.support**

- jdbc.core 및 jdbc.object를 사용하는 JDBC 프레임워크를 지원

## DTO(Data Transfer Object)

- 컨트롤러 뷰, 비즈니스 계층, 퍼시스턴스 계층 등 계층 간 데이터 교환을 위한 자바빈즈
- 일반적으로 DTO는 로직을 가지고있지 않고 순수한 데이터 객체이다.
- 보통 필드와 getter, setter를 가지고 추가적으로 toString(), equals(), hashCode()등의 Object 메소드를 오버라이딩 할 수 있다.

## DAO(Data Access Object)

- 데이터를 조회하거나 조작하는 기능을 전담하는 객체

## Connection Pool

- DB 연결은 비용을 많이 소모하기 때문에 커넥션 풀이 미리 커넥션을 여러 개 맺어놓고 커넥션이 필요하면 커넥션 풀에게 빌려서 사용하고 반납하는 방법을 사용한다.

### DataSource

- 커넥션 풀을 관리하는 목적으로 사용되는 객체
- DataSource를 이용하여 커넥션을 빌려오고 반납한다.
