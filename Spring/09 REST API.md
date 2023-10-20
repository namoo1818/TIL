### 2023.10.20
# REST(Representational State Transfer)
- 2000년도 로이 필딩(Roy Fielding)의 박사학위 논문에 최초로 소개
- REST는 'Representational State Transfer'의 약어로 하나의 URI는 하나의 고유한 리소스(Resource)를 대표하도록 설계된다는 개념에 전송방식을 결합해서 원하는 작업을 저장한다
- 웹의 장점을 최대한 활용할 수 있는 아키텍처(설계구조)로써 REST를 발표
- HTTP URI를 통해 제어할 자원(Resource)를 명시하고, HTTP Method(GET, POST, PUT, DELETE, PATCH)을 통해 해당 자원(Resource)를 제어하는 명령을 내리는 방식의 아키텍처 
- 우리는 PATCH 안한다

# REST 구성
- 자원(Resource): URI
- 행위(Verb): HTTP Method
- 표현(Representations)

- 잘 표현된 HTTP URI로 **리소스를 정의**하고 HTTP method로 리소스에 대한 **행위를 정의**한다
- 리소스는 JOSN, XML과 같은 여러가지 언어로 **표현**할 수 있다.
- URI + (GET/POST/PUT/DELETE)

# 기존의 웹 접근 방식과 REST API 방식의 차이점
![table](https://github.com/namoo1818/TIL/assets/50236187/fd0e671c-bc4c-4ff7-a138-32ed2eca6062)
- 기존의 접근 방식은 GET과 POST만으로 자원에 대한 CRUD를 처리하며, URI는 액션을 나타냄
- REST로 변경할 경우 4가지 method를 모두 사용하여 CRUD를 처리하며, URI는 제어하려는 자원을 나타냄
- REST 방식에서 writeform 같은건 프론트가 한다

# API(Application Programming Interface)
- 두 소프트웨어 요소들이 서로 통신할 수 있게 하는 방식(예: 미세먼지 정보 제공 시스템, 핸드폰 정보 미세먼지 앱)
- Application은 고유한 기능을 가진 모든 소프트웨어
- Interface는 두 애플리케이션 간의 요청과 응답에 의한 통신하는 방법

#  API 유형
- 프라이빗 API
  - 기업 내부에 있으며 비즈니스 내에서 시스템과 데이터를 연결하는데 사용
- 퍼블릭 API
  - 일반에게 공개되며 누구나 사용할 수 있다
  - 단, 사용에 대한 권한 설정과 비용이 있을 수도 있다
  - 공공데이터 포털, 기상청, Naver, Kakao, Youtube 등 대부분이 REST 방식으로 작성
  - 주로 json형태로 data만 준다.

# REST API(REST+API)
- 기존의 전송방식에서 서버는 클라이언트에게 데이터와 화면을 전송하였다
- REST API 방식에서 서버는 클라이언트에게 요청 받은 리소스에 대해 순수한 데이터만 전송한다. 화면은 클라이언트의 몫.
- HTTP URI를 통해 제어할 자원(Resource)을 명시하고, HTTP METHOD(GET/POST/PUT/DELETE)를 통해 해당 자원(Resource)를 제어하는 명령을 내리는 방식의 Architecture.
- 가장 큰 단점: 표준이 없다. 암묵적인 약속만 있다.
  - 하이픈(-) 사용 가능, 언더바(_) 사용 안함
  - 대문자 사용 안함
  - URI 마지막에 슬래시(/) 사용 안함
  - 슬래시(/)로 계층 관계 표시
  - 확장자가 포함된 파일 이름을 직접 포함시키지 않음
  - URI는 명사 사용

# REST API 흐름
- 예전에는 서버가 클라이언트에게 HTML, CSS, JS로 이루어진 완성된 페이지(정적 페이지)를 넘겨주었다
- 데이터가 실시간으로 변하는 동적페이지는 어떻게?
- 페이지(index.html)를 하나만 만들어놓고 부품을 교체하는 방식으로 하자! -> SPA(Single Page Application) -> 우리는 Vue.js로 한다
- 위 방식은 처음 로딩 시간이 길지만 그 다음부터는 부품만 교체하면 되기 때문에 빠르다
- 클라이언트가 사용할 수 있는 언어 JavaScript. 실시간으로 클라이언트가 서버에 데이터를 넘겨주는 방식 AJAX.
- PC, 모바일, TV, 탭 등 기기마다 화면 크기가 다르다. -> 반응형 웹의 등장 -> 서버는 데이터만 줄게. 너가 화면 만들엉.

![흐름](https://github.com/namoo1818/TIL/assets/50236187/cebc3455-538c-47a9-a4a9-6ed6149f4eca)

# 기존의 Service와 REST API Service
![service](https://github.com/namoo1818/TIL/assets/50236187/c1ae4642-c1bb-4a49-abcc-0c03e06bc907)
- PC인지 모바일인지 TV인지 신경쓸 필요가 없어졌다
![웹서비스](https://github.com/namoo1818/TIL/assets/50236187/08602d85-ecc6-4a1c-b4ae-26d5c1b736e6)
- 우리는 현재 컴퓨터 한대로 4대를 돌리고 있다(백엔드, 프론트엔드, 서버, 기존)

# Spring REST 관련 Annotation 및 클래스
![클래스](https://github.com/namoo1818/TIL/assets/50236187/2bd8f46d-3187-435b-bd63-5959aa5a5bbe)
- 동일출처원칙: 한 페이지에서는 하나의 서버에서만 데이터를 가져와서 사용해야 한다
- 하지만 여러 서버에서 데이터를 가져와서 사용하고 싶은걸...이것을 해결해주는 것이 @CrossOrigin

# 실습
- 크롬에서 Talend API Tester 설치
- TestController.java
```java
@Controller
public class TestController1 {
//	http://localhost:8080/mvc/rest1/test1 : 404 에러 화면, 뷰리졸버가 반환된 문자열을 가지고 View 를 찾으려고 해서...
	@GetMapping("/rest1/test1")
	public String test1() {
		return "hi rest";
	}
	
//	http://localhost:8080/mvc/rest1/test2 : @ResponseBody를 붙여서 JSP 화면으로 반환하는게 아니라 데이터 그자체를 반환
	@ResponseBody
	@GetMapping("/rest1/test2")
	public String test2() {
		return "hi rest";
	}
	
}
```
- localhost:8080은 톰캣이 자동으로 설정해준다

- 406 에러. 왜? Map 형태의 데이터를 리턴해서. JSON 형태로 바꿔져야 한다
```java
// http://localhost:8080/mvc/rest1/test3 : 406 에러. 데이터를 JSON 형태로 바꿔야 한다 
@ResponseBody
@GetMapping("/rest1/test3")
public Map<String, String> test3() {
	// 키 벨류 형태를 가지고 있는 앱을 반환
	Map<String, String> data = new HashMap<String, String>();
	
	data.put("id", "ssafy");
	data.put("password", "1234");
	data.put("name", "양띵균");
	return data;
}
```
- JSON 형변환을 위해 pom.xml에 jackson-databind 추가
```xml
<!-- JSON 형변환을 위하여 -->
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
	<version>2.14.2</version>
</dependency>
```
- JACKSON이 알아서 Map을 JSON 형태로 바꿈
![200](https://github.com/namoo1818/TIL/assets/50236187/677cac8a-b2a9-42e1-a4f8-dcf1cb3b322d)
- DTO 객체, 리스트도 JACKSON이 알아서 JSON 형태로 바꿔준다 잭슨 짱!
```java
//http://localhost:8080/mvc/rest1/test4 : 잭쓴이 DTO오 알아서 JSON으로 바꿔서 보내주는군 GOOD!
@ResponseBody
@GetMapping("/rest1/test4")
public User test4() {
	User user = new User("ssafy", "1234", "양띵균");
	return user;
}

//http://localhost:8080/mvc/rest1/test5 : LIST 도 반환 해주나?
@ResponseBody
@GetMapping("/rest1/test5")
public List<User> test5() {
	List<User> list = new ArrayList<>();
	list.add(new User("ssafy", "1234", "양띵균"));
	list.add(new User("hyunsoo", "3141592", "조현수"));
	list.add(new User("s4253541", "secret", "조용환"));
	list.add(new User("enugg", "1234", "김은지"));
	list.add(new User("dawon", "1008", "차다운"));
	
	return list;
}
```
- 아...쓰읍...메서드마다 @ResponseBody 붙이는거 에반데...
- @RestController를 사용하면 @ResponseBody 안써도 된다
- RestController가 있어서 test1도 실행된다 @ResponseBody가 붙어있는 것과 같기 때문에
```java
@RestController
@RequestMapping("/rest2")
public class TestController2 {
//	http://localhost:8080/mvc/rest2/test1 : RestController가 있어서 test1도 실행된다  @ResponseBody가 붙어있는 것과 같다
	@GetMapping("/test1")
	public String test1() {
		return "hi rest";
	}
	
//	http://localhost:8080/mvc/rest2/test2 : @ResponseBody를 붙여서 JSP 화면으로 반환하는게 아니라 데이터 그자체를 반환
	@GetMapping("/test2")
	public String test2() {
		return "hi rest";
	}
	
//	http://localhost:8080/mvc/rest2/test3 : 406 에러. 데이터를 JSON 형태로 바꿔야 한다 
	@GetMapping("/test3")
	public Map<String, String> test3() {
		// 키 벨류 형태를 가지고 있는 앱을 반환
		Map<String, String> data = new HashMap<String, String>();
		
		data.put("id", "ssafy");
		data.put("password", "1234");
		data.put("name", "양띵균");
		return data; //jackson-databind을 추가해주었더니 map을 알아서 json으로 바꿔서 줌
	}
...
```
