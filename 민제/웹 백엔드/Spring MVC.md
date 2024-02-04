# Spring MVC(Model-View-Controller)

- Model : 모델은 뷰가 렌더링하는데 필요한 데이터이다. 예를 들어 사용자가 요청한 상품 목록이나, 주문 내역이 이에 해당한다.
- View : 웹 애플리케이션에서 뷰(View)는 실제로 보이는 부분이며, 모델을 사용해 렌더링을 한다. 뷰는 JSP, JSF, PDF, XML등으로 결과를 표현한다.
- Controller : 컨트롤러는 사용자의 액션에 응답하는 컴포넌트이다. 컨트롤러는 모델을 업데이트하고, 다른 액션을 수행한다.

## DispatcherServlet**

- 프론트 컨트롤러 (Front Controller)
- 클라이언트의 모든 요청을 받은 후 이를 처리할 핸들러에게 넘기고 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여준다.
- DispathcerServlet은 여러 컴포넌트를 이용해 작업을 처리한다.

<img width="685" alt="image" src="https://github.com/alswp006/23-winter-project-study/assets/102672547/49afa43b-a7a3-4e04-9734-58d6806bed01">

### 아티팩트 생성 참고

https://getinfo.tistory.com/2
