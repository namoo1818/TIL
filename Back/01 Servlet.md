### 2023.09.05
# 웹프로그래밍
#### 웹 등장 전
- 한 컴퓨터가 프로그램을 잘 만듦
- 컴퓨터 A: 나줘!
- 컴퓨터 B: 나도 줘!
- 프로그램을 물리적으로 전달함 
#### 웹 등장 후
- 요청(request)과 응답(response)이 등장
- 그에 따라 약속도 생김 그것이 http
- ?: 아 프로그램 다 주는거 에반데;; 힘들어
- 컴퓨터마다 HTML, CSS, JS를 가지고 서버는 data만 전달
- 서버를 만드는 사람을 서버개발자 BackEnd 개발자, 화면에 보여주는 것들을 만드는 사람 FrontEnd 개발자
- 서버 배포 AWS
- client와 server를 연결하는 프로그램 AJAX
- JS 프로그램 Vue.js
- server 프로그램 Spring
- DB 프로그램 Mybatis

<img href="웹프로그래밍" src="https://github.com/namoo1818/TIL/assets/50236187/e47f7f9f-c109-4924-a8f9-a8b75a62b6e9" width=600><br>
<img href="웹 아키텍쳐" src="https://github.com/namoo1818/TIL/assets/50236187/280dd70d-7452-4f0e-b519-58777e99a7c6" width=700><br>

### WAS
- webserver와 Application Server를 합친 것
- Web Application Server
- WAS도 종류가 많지만 우리는 Tomcat를 사용한다

## 웹과 웹 프로그래밍
- URL(Uniform Resource Locator) - 웹 상의 자원을 참조하기 위한 웹 주소, URI의 한 종류
- 웹 페이지(Web page) - 웹 브라우저를 통해서 보여지는 화면
- 웹 서버(Web Server) - 클라이언트 요청에 맞는 응답(웹 페이지)을 제공
- 웹 어플리케이션(Web Application) - 웹 서버를 기반으로 실행되는 응용 소프트웨어
- 웹 어플리케이션 서버(Web Application Server, WAS) - 요청이 오면 알맞는 프로그램을 실행하여 응답 만들고 제공하는 서버

# Dynamic Web Project 구조
![dynamic web project](https://github.com/namoo1818/TIL/assets/50236187/8037386d-069c-4a5d-969b-0f95067fc764)

# 서블릿(Servlet)
- Server + Applet의 합성어
- 자바를 이용하여 웹에 실행되는 프로그램을 작성하는 기술
- 자바를 이용하여 웹페이지를 동적으로 생성할 수 있음
- Servlet은 자바 코드 안에 HTML을 포함
- 우리는 이미 만들어진 Servlet API를 사용할 것임

# HelloServlet
- Context root: BackEnd_Day00_Hello
- Content directory : WebContent
  
- 여러 프로젝트를 Tomcat에 올려서 실행하는데 프로젝트를 구분하기 위해서 context root 사용
- http://localhost:8080/BackEnd_Day00_Hello/HelloServelt
- http://localhost:8080/[프로젝트명]/[요청]
  
- WebContent : 웹에서 보여지는 것들(HTML, CSS,..)이 모여있는 폴더
  
- web.xml : 설정 모음(옛날 방식)
- welcome-file 리스트를 위에서부터 차례대로 찾으면서 파일이 있으면 띄어줌

- https://javaee.github.io/javaee-spec/javadocs/
- 여기 한번씩 읽어보는게 좋다 물론 영어임

# Interface Servlet
- destroy, getServletConfig, getServletInfo, init, service 메서드를 구현해야함
```java
// 해당 클래스를 서블릿으로 만들기 위해서는 Servlet을 구현해야한다
public class MyServlet1 implements Servlet {

	@Override
	public void destroy() {
		// 서블릿이 소멸할 때 동작
		
	}

	@Override
	public ServletConfig getServletConfig() {
		// 서블릿 설정 반환
		return null;
	}

	@Override
	public String getServletInfo() {
		// 서블릿 정보를 문자열로 반환
		return null;
	}

	@Override
	public void init(ServletConfig arg0) throws ServletException {
		// 서블릿을 초기화
		
	}

	@Override
	public void service(ServletRequest arg0, ServletResponse arg1) throws ServletException, IOException {
		// 여기에서 요청과 응답을 처리
		
	}

}
```

# Class GenericServlet
- 인터페이스 서블릿을 구현할게 너무 많아
- service 메서드만 구현해도 돼
```java
public class MyServlet2 extends GenericServlet {

	// 객체 직렬화, 해도 되고 안해도 상관없음
	private static final long serialVersionUID = 1L;

	@Override
	public void service(ServletRequest arg0, ServletResponse arg1) throws ServletException, IOException {
		// 서비스 구현	
	}
}
```

# Class HttpServlet
- doGet, doPost, doPut, doDelete 중 적어도 하나 구현해야함
```java
public class MyServlet3 extends HttpServlet {

	private static final long serialVersionUID = 1L;

	// doXXXXX 이런거 한개는 만들어야 한다

}
```

# 고전 방식
- web.xml에 등록
```java
package com.ssafy.myservlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

// 고전 방식으로 등록해보자
public class MyServlet4 extends HttpServlet {

	private static final long serialVersionUID = 1L;

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		PrintWriter writer = response.getWriter();
		writer.append("<html>");
		writer.append("<head>");
		writer.append("<title>Hello</title>");
		writer.append("</head>");
		writer.append("<body>");
		writer.append("<h1>Hello Servlet4</h1>");
		writer.append("</body>");
		writer.append("</html>");
	}

}

```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>BackEnd_Day01_Servlet</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
  <servlet>
    <servlet-name>MyServlet</servlet-name>
    <servlet-class>com.ssafy.myservlet.MyServlet4</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>MyServlet</servlet-name>
    <url-pattern>/MyServlet</url-pattern>
  </servlet-mapping>
</web-app>
```
![servlet4](https://github.com/namoo1818/TIL/assets/50236187/881155e5-9fd7-4a6a-b5a5-851aadcc529d)

# 최신 방식
- Annotation 사용
- xml에 등록하지 않아도 됨
```java
package com.ssafy.myservlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

// 최신 기술
@WebServlet("/MyServlet2")
public class MyServlet5 extends HttpServlet {

	private static final long serialVersionUID = 1L;

	@Override
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		PrintWriter writer = response.getWriter();
		writer.append("<html>");
		writer.append("<head>");
		writer.append("<title>Hello</title>");
		writer.append("</head>");
		writer.append("<body>");
		writer.append("<h1>Hello Servlet5</h1>");
		writer.append("</body>");
		writer.append("</html>");
	}

}
```
![servlet5](https://github.com/namoo1818/TIL/assets/50236187/28531419-7504-4b66-9dd4-d3300aca1c01)

# Servlet 생명주기
![생명주기](https://github.com/namoo1818/TIL/assets/50236187/574fb374-925d-4506-b2a1-979c8241b015)
- 1,2,3,5번은 딱 한번만 수행
- 서비스 메서드는 지속적으로 살아있으면서 요청이 있을 때마다 실행된다

# Servlet Parmeter
## GET과 POST
![get과 post](https://github.com/namoo1818/TIL/assets/50236187/df8e75f4-7694-4de0-ac62-1cbf2d4cb744)
- C R U D
- GET에서는 주로 Read
- POST에서는 Create, Update, Delete
- 로그인은 url에 정보가 유출되면 안되므로 post로


## URL 구성요소
![url](https://github.com/namoo1818/TIL/assets/50236187/6e1d90eb-981d-43bf-b230-767617f49307)
- URL에는 IP주소 또는 돈주고 산 도메인이 들어온다    
`http://서버/[컨루;컨텍츠 루트]/경로?key=value&key2=value`
- 프로젝트 파일 우클릭>web context 어쩌구에서 context root를 바꿀 수 있다
- ? 다음부터는 처리하기 위한 key와 value가 나온다    
`https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query=ssafy`


### method="GET"
```html
<h2>GET Form</h2>
<form action="" method="GET">
	<!-- name 속성필요. -->
	<input type="text" name="id">
	<input type="submit">
	<button>보내</button>
</form>
```
- form action = "" : 해당 주소(경로)로 다시 한번 요청을 보내줘 디폴트는 ""(현재주소)
- method="GET" : get이나 post가 올 수 있다 디폴트는 get 방식
- input type="text" 
- name은 key
- 작성한 내용이 value
- form 태그는 따로 설정하지 않으면 submit처럼 작동
- \<input type="submit">과 \<button>은 같은 역할

- id에 "ssafy", pw에 "1234" 입력하고 제출했다면 주소는 다음과 같다    
`http://localhost:8080/gogo?id=ssafygr&pw=1234`   
- url에 정보가 다 보인다


### method="POST"
```html
<h2>POST Form</h2>
<form action="" method="POST">
	<!-- name 속성필요. -->
	<input type="text" name="id"> 
	<input type="submit">
</form>
```
- id에 "ssafy", pw에 "1234" 입력하고 제출했다면 주소는 다음과 같다     
`http://localhost:8080/gogo`
- url에 노출되지 않는다
- 물론 POST 방식도 개발자모드>Nextwork 에 다 출력된다 그래서 비밀번호같은 정보는 암호화해서 전달해야 한다
- 로그인같은 개인정보는 url에 유출되면 안되므로 post로 설정
- post 방식으로 오는 한글은 깨질 수 있으므로 utf-8 설정을 따로 해줘야한다

### / 유무 차이
```html
<!-- 차이를 느껴라! -->
<h2>Action1</h2>
<form action="/gogo" method="GET">
	<!-- name 속성필요. -->
	<input type="text" name="id">
	<input type="password" name="pw">
	<input type="submit">
</form>
<h2>Action2</h2>
<form action="gogo" method="GET">
	<!-- name 속성필요. -->
	<input type="text" name="id">
	<input type="password" name="pw">
	<input type="submit">
</form>
```
- / 있으면 Content root가 생략되고 포트 번호 바로 다음에 어노테이션 주소가 뜸       
`http://localhost:8080/gogo?id=&pw=`     
- / 없으면 Content root 다음으로 어노테이션 주소가 뜸      
`http://localhost:8080/BackEnd_Day01_Servlet/gogo?id=&pw=`

# Servlet Parameter
## GET 방식
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	String text = request.getParameter("text");
	
	response.setContentType("text/html; charset=UTF-8");
	
	PrintWriter writer = response.getWriter();
	writer.append("<html>");
	writer.append("<head>");
	writer.append("<title>Hello</title>");
	writer.append("</head>");
	writer.append("<body>");
	writer.append("<h1>"+text+"</h1>");
	writer.append("</body>");
	writer.append("</html>");
}
```

## POST 방식
- post 방식은 request이 utf-8로 잘 작동하지 않을 수 있기 때문에 따로 설정
```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	request.setCharacterEncoding("UTF-8");
}
```

# front-controller 
- 웹에서 발생하는 모든 요청에 대해 호출되는 Servlet을 만들어 처리함
- 어떤 요청을 보내면 관련 서블릿이 동작을 하게끔 하는 무적의 서블릿
```java
@WebServlet("/main")
public class MainServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public MainServlet() {
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setContentType("text/html; charset=UTF-8");
		doProcess(request, response);
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		request.setCharacterEncoding("UTF-8");
		doGet(request, response);
	}

	private void doProcess(HttpServletRequest request, HttpServletResponse response) throws IOException {
		String action = request.getParameter("action");

		switch (action) {
		case "regist":
			doSignup(request, response);
			break;
		case "gugu":
			doGugu(request, response);
			break;
		default:
			break;

		}
	}

	private void doGugu(HttpServletRequest request, HttpServletResponse response) throws IOException {
		// 생략

	}

	private void doSignup(HttpServletRequest request, HttpServletResponse response) throws IOException {
		// 생략

	}

}
```


# 기타
- 스프링부트에는 톰캣이 내장되어 있다
- jsp 나중에 관통 프로젝트에는 쓰지 않는다
- 면접 질문 : 크롬을 키고 네이버에 "구글"을 검색했습니다. 무슨 일이 발생하나요?

