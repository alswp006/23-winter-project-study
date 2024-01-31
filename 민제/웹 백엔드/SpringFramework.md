# Spring Framework

- 엔터프라이즈급 어플리케이션(거대한 어플리케이션)을 구축할 수 있는 가벼운 솔루션이자, 원스-스탑-숍(One-Stop-Shop)(모든 과정을 한꺼번에 해결하는 상점)
- 원하는 부분만 가져다 쓸 수 있도록 모듈화가 잘 되어 있다. → 가벼운 솔루션 (약 20개의 모듈로 구성되어 있다.)
- IoC(Inversion of Control) 컨테이너이다.
- 선언적으로 트랜잭션을 관리할 수 있다.
- AOP를 지원한다.
- 완전한 기능을 갖춘 MVC Framework를 제공한다.

## AOP와 Instrumentation

- spring-AOP : AOP 얼라이언스(Alliance)와 호환되는 방법으로 AOP를 지원한다.
- spring-aspects : AspectJ와의 통합을 제공한다.
- spring-instrument : 인스트루멘테이션을 지원하는 클래스와 특정 WAS에서 사용하는 클래스로 더 구현체를 제공한다. BCI(Byte Code Instrumentations)는 런타임이나 로드(Load) 때 클래스의 바이트 코드에 변경을 가하는 방법을 말한다.

## **메시징(Messaging)**

- spring-messaging : 스프링 프레임워크 4는 메시지 기반 어플리케이션을 작성할 수 있는 Message, MessageChannel, MessageHandler 등을 제공합니다. 또한, 해당 모듈에는 메소드에 메시지를 맵핑하기 위한 어노테이션도 포함되어 있으며, Spring MVC 어노테이션과 유사합니다.

## **데이터 엑서스(Data Access) / 통합(Integration)**

- 데이터 엑세스/통합 계층은 JDBC, ORM, OXM, JMS 및 트랜잭션 모듈로 구성되어 있다.
- **spring-jdbc** : 자바 JDBC프로그래밍을 쉽게 할 수 있도록 기능을 제공합니다.
- **spring-tx** : 선언적 트랜잭션 관리를 할 수 있는 기능을 제공합니다.
- spring-orm : JPA, JDO및 Hibernate를 포함한 ORM API를 위한 통합 레이어를 제공합니다.
- spring-oxm : JAXB, Castor, XMLBeans, JiBX 및 XStream과 같은 Object/XML 맵핑을 지원합니다.
- spring-jms : 메시지 생성(producing) 및 사용(consuming)을 위한 기능을 제공, Spring Framework 4.1부터 spring-messaging모듈과의 통합을 제공합니다.

## **웹(Web)**

- 웹 계층은 spring-web, spring-webmvc, spring-websocket, spring-webmvc-portlet 모듈로 구성됩니다.
- **spring-web** : 멀티 파트 파일 업로드, 서블릿 리스너 등 웹 지향 통합 기능을 제공한다. HTTP클라이언트와 Spring의 원격 지원을 위한 웹 관련 부분을 제공합니다.
- **spring-webmvc** : Web-Servlet 모듈이라고도 불리며, Spring MVC 및 REST 웹 서비스 구현을 포함합니다.
- spring-websocket : 웹 소켓을 지원합니다.
- spring-webmvc-portlet : 포틀릿 환경에서 사용할 MVC 구현을 제공합니다.

## IoC와 Container

### Container

- 인스턴스의 생명 주기 관리
- 생성된 인스턴스들에게 추가 기능 제공

### IoC(Inversion of Control)

- 제어의 역전
- 개발자가 프로그램의 제어를 하는 것이 아니라 다른 프로그램이 흐름을 제어하는 것

### DI (Dependency Injection)

- 의존성 주입
- 클래스 사이의 의존 관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
- DI 예
    - DI 미적용
        
        ```java
        class 엔진{}
        class 자동차{
        	엔진 v5 = new 엔진();
        }
        ```
        
    - DI 적용
        
        ```java
        @Component
        class 엔진{}
        
        @Component
        class 자동차{
        	@Autowired
        	엔진 v5; //spring container가 인스턴스를 할당해준다.
        }
        ```
        

### **Spring에서 제공하는 IoC/DI 컨테이너**

- BeanFactory : IoC/DI에 대한 기본 기능을 가짐
- ApplicationContext : BeanFactory의 모든 기능을 포함하며, 일반적으로 BeanFactory보다 추천된다. 트랜잭션처리, AOP등에 대한 처리를 할 수 있고 BeanPostProcessor, BeanFactoryPostProcessor등을 자동으로 등록하고, 국제화 처리, 어플리케이션 이벤트 등을 처리할 수 있다.
    - BeanPostProcessor : 컨테이너의 기본로직을 오버라이딩하여 인스턴스화와 의존성 처리 로직 등을 개발자가 원하는 대로 구현 할 수 있게 해준다.
    - BeanFactoryPostProcessor : 설정된 메타 데이터를 커스터마이징 할 수 있다.
