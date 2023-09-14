### 2023.09.14
# Spring MVC
## MVC 요청 흐름
![mvc요청흐름](https://github.com/namoo1818/TIL/assets/50236187/11e8014f-c7cc-4341-99a2-d62561efa4bf)
- 클라이언트가 요청을 하면 servlet이 가장 먼저 동작함
- 만약 Servlet이 없다? Life Cycle에서 하나 만듦
- Front-controller 패턴
```java
class MyServlet extends HttpServlet {
  doGet(요청, 응답)
  doPost(요청, 응답)
  deProcess(요청, 응답) 
```
- Servlet은 List를 관리하고 있는 Manager에게 요청함
- forward: 응답과 요청이 있는 통로가 이어진다
- redirect: 클라이언트에게 응답을 돌려주면서 통로를 새로 뚫는다
- jsp 파일을 사용자에게 던져준다

- Cotroller
- Model
- View

- 데이터는 내가 줄게 view는 사용자가 직접 만들어! view 만들 수 있는 언어는 js가 유일..다 만들기 힘드렁 이미 만들어진 프레임워크 Vue.js를 쓸 것이다

# Spring MVC 요청 흐름
![spring mvc](https://github.com/namoo1818/TIL/assets/50236187/8c79dfa4-ecd5-4ade-85c6-bb0a4e0012cf)
- Spring의 특징: POJO(순수하다는 뜻)
- class MyController 뒤에 extends와 같은 것들이 붙지 않고 순수한 클래스를 만들어 쓸 수 있어야 한다
- MyController에 @Controller 설정
- Model 영역은 크게 Service 영역과 Repository(DaO) 영역으로 나눌 수 있다
- Repository(DaO): Data Acess Object의 약자
- DTO: Data Transfer Object
- Controller는 필드로 service를 가지고 있어야 이 안에서 메서드가 동작할 때 요청 가능
- service를 어떻게 넣을건데? @Autowired로
- controller도 servlet과 마찬가지로 여러개가 있을 수 있다
- 하지만 Spring MVC는 front controller 패턴을 가지고 있다: 맨 앞에 controller와 view에 연결해주는 디스패쳐 서블릿이라는 대표가 있다
- 컨셉은 싱글턴이였으니 따로 싱글턴 처리를 해주지 않아도 괜찮다

# Model
- 동작을 수행하는 코드
- 사용자 View(jsp)
- 

# View
- 사용자가 화면에 무엇을 어떻게 볼 것인지를 결정 -> UI/UX
- 사용자 회면에 보이는 부분
- 모델의 정보를 받아와 사용자에게 보여주는 역할 수행
- 자체적으로 모델의 정보를 보관 x

# Controller
- 모델과 뷰를 연결하는 역할을 수행
- 사용자에게 데이터를 가져오고 수정하고 제공함
- Controller는 절대로 DAO로 바로 가지 않는다 Controller는 Service를 부르고 Service에서 dao를 부르고 dao에서 db로 왔다갔다 한다 
- Service에서 작성하는 메서드명은 사용자친화적으로 작성하고 Dao에서 작성하는 메서드명은 DB친화적으로 작성한다

# Spring Web MVC(Spring MVC)
-
-
-
- Dispatch
- 다른 프레임워크와 마찬가지로 front
- 중심이 되는

# Spring MVC 구성
## DispatcherServlet
- Servlet WepApplicationContext: web 직접 관련
- Root WebApplicationConext: 그 외

- ​ModelAndView: 컨트롤러는 요청에 따라 어떤 뷰에 어떤 데이터(모델)을 가지고 응답해야 하는지 알려주는 것입니다 그래서 Model and View를 알려주는 거예요
- Model And View : 데이터, 뷰이름

# Spring MVC 요청 처리 흐름

# Servlet 등록하는 방법
1. web.xml
2. @Annotation

# Spring Web MVC 구성하기 3
- **DefaultAnnotationHandlerMapping을 기본으로 사용하므로 별도 등록없이 사용가능**
