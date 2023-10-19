### 2023.10.19
# 요청의 흐름
![mvc흐름](https://github.com/namoo1818/TIL/assets/50236187/eb4b6b8e-d5ef-40cd-9aa4-4e694c621a60)

- 우리는 현재 `Client, Server, DB`를 한 컴퓨터로 돌리고 있다 원래는 전부 별개의 컴퓨터다.
- 클라이언트가 서버에 `request(요청)`을 보낸다.(`GET`이나 `POST` 방식으로)
  - GET은 URI에 정보가 포함되고 POST에는 포함되지 않는다.
  - GET은 READ할 때, POST는 CREATE, UPDATE, DELETE할 때 주로 사용한다.
- 클라이언트와 서버 사이에 `필터`를 넣을 수 있다. 스프링에서는 캐릭터 인코딩 필터인 UTF-8 문자 인코딩을 사용한다.
- `Dispatcher Servlet`을 제일 먼저 만난다. 디패서는 설정 파일 2개(servlet-context.xml, root-context.xml)가 있다.
  - `servlet-context.xml`: 웹 관련 설정
  - `root-context.xml`: 그 외 설정
- `핸들러매핑` `컨트롤러`로 간다. 컨트롤러는 servlet-context에 등록한다.
- 컨트롤러는 `xxxService`를 가지고 있다. xxxService는 root-context에 등록한다. xxxService는 사용자친화적으로 만든다. 
- 컨트롤러는 xxxService를 의존성 주입으로 가지고 있다. 의존성 주입으로 `@Autowired`를 사용한다.
  - @Autowired 사용 방법 1. 필드 2. 설정자 주입 3. 생성자 주입
- xxxService는 DB를 이용하기 위해 `xxxDao(Repsitory)`를 부른다. xxxDao는 root-context에 등록한다.
- xxxDao와 DB와 데이터를 주고 받는다. 처음에는 프레임워크로 JDBC를 썼다가 지금은 더 편한 `MyBatis`를 사용한다
  - MyBatis는 root-context에 등록한다.
  - MyBatis는 Interface + mapper.xml 구현체를 만든다.
- `mapper`는 namespace가 무조건 있어야한다.  
  - mapper에는 \<select> \<insert> \<update> \<delete> 태그를 사용할 수 있다.
  - type(클래스 그자체)과 map(우리가 만든 형식)으로 구분해서 사용한다.
  - 동적쿼리도 가능하다.
  - ${}: 파라미터가 바로 출력, 해당 컬럼의 자료형에 맞추어 파라미터 자료형이 변경된다. 테이블이나 컬럼명을 파라미터로 전달하고 싶을 때 사용, 쿼리 주입 예방 불가능, 보안에 불리
  - #{}: 파라미터가 String 형태로 들어와 자동으로 파라미터 형태가 됨. 쿼리 주입을 예방할 수 있어 보안에 유리
- 데이터를 주고받을 때 DTO을 사용한다
- 컨트롤러에서 반환타입은 크게 Model&View과 String가 있다. 실제로는 디패서로 Model&View 객체가 반환된다.
- 컨트롤러에서 디패서로 반환할 때 `인터셉터`가 동작한다. 인터셉터는 servlet-context에 등록한다.
  - 인터셉터 기능 3가지: pre, post, after
  - pre만 유일하게 boolean타입 반환. 예외발생시 after는 파리미터에 값이 채워지고(평소에는 null), post는 동작하지 않는다.
- 디패서에 M&V 객체가 반환되면 디패서는 `View Resolver`를 동작시킨다. View Resolver(profix, suffix)는 servlet-context에 등록한다. View Resolver는 view name를 리턴한다.
- 디패서는 Model에 담겨있던 `View`를 동작시킨다. View는 xx.jsp(EL, JSTL)를 완성시킨다.
  - 우리는 JSTL에서 core를 가장 많이 썼다
  - xx.jsp 4가지 영역: page / request / session / application
- 사용자에게 response 응답을 준다

# 컨트롤러
- 컨트롤러에서 @Request Mapping을 쓰다가 더 진보된 방식인 @GetMapping(경로), @PostMapping(경로)을 사용한다. 역할은 완전히 똑같다.
- 컨트롤러에서 메서드를 사용할 수 있다.
  - request, response, httpsession, Model(바구니), sqlString, DTO(바구니) 등을 매개변수로 사용할 수 있다.
  - 리턴 방식 1. forward 2. redirect:요청이름(클라이언트가 요청 다시 보냄)
