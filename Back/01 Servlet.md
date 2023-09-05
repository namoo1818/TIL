### 2023.09.05
# 웹프로그래밍

- URL(Uniform Resource Locator) - 웹 상의 자원을 참조하기 위한 웹 주소, URI의 한 종류(다른 하나는 URN)
- 웹 페이지

- Context root: BackEnd_Day00_Hello
- 여러 프로젝트를 Tomcat에 올려서 실행하는데 프로젝트를 구분하기 위해서 context root 사용
- http://localhost:8080/BackEnd_Day00_Hello/HelloServelt
- http://localhost:8080/[프로젝트명]/[요청]


- 로그인은 url에 정보가 유출되면 안되므로 post로

- get와 post
- C R U D


https://javaee.github.io/javaee-spec/javadocs/
Servlet
Class HttpServlet

<h2>Action1</h2>
	<form action="/gogo" method="GET">
		<!-- name 속성필요. -->
		<input type="text" name="id">
		<input type="password" name="pw">
		<input type="submit">
	</form>
http://localhost:8080/gogo?id=ssafygr&pw=





<h2>Action2</h2>
	<form action="gogo" method="GET">
		<!-- name 속성필요. -->
		<input type="text" name="id">
		<input type="password" name="pw">
		<input type="submit">
	</form>
http://localhost:8080/BackEnd_Day01_Servlet/gogo?id=ssfrr&pw=


- URL에는 IP주소 또는 돈주고 산 도메인이 들어온다
- http://서버/[컨루;컨텍츠 루트]/경로?key=value&key2=value
- ? 다음부터는 처리하기 위한 key와 value가 나온다 
https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query=ssafy

- 프로젝트 파일 우클릭>web context 어쩌구에서 context root를 바꿀 수 있다

- 스프링부트에는 톰캣이 내장되어 있다
- 

- form 어쩌구 html 파일
- form action = "" : 해당 주소(경로)로 다시 한번 요청을 보내줘 디폴트는 ""
- method="GET" : get이나 post가 올 수 있다 디폴트는 get 방식
- input type="text" 
- name : 키
- form 태그는 따로 설정하지 않으면 submit처럼 작동

- 보내면 개발자 모드>network에 출력됨>로그인같은 개인정보는 암호화 필요

- post 방식으로 오는 한글은 깨짐

- post 방식은 request utf-8이 잘 작동하지 않을 수 있다 따로 선언?

front-controller 
요청을 구구단, 회원가입 등 여러 서블릿에 보내지 않고 하나의 서블릿에서 보냄

jsp 나중에 관통 프로젝트에는 쓰지 않는다


면접 질문
크롬을 키고 네이버에 "구글"을 검색했습니다. 무슨 일이 발생하나요?
