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
- 웹 페이지




- Context root: BackEnd_Day00_Hello
- 여러 프로젝트를 Tomcat에 올려서 실행하는데 프로젝트를 구분하기 위해서 context root 사용
- http://localhost:8080/BackEnd_Day00_Hello/HelloServelt
- http://localhost:8080/[프로젝트명]/[요청]


- https://javaee.github.io/javaee-spec/javadocs/
- 여기 한번씩 읽어보는게 좋다 물론 영어임
- javax.servlet > Interfaces 


- 고정 방식 : 실습파일 MyServlet4
- 최신 방식 : @WebServlet 사용 실습파일 MyServlet5

# Servlet 생명주기
이미지추가
- 서비스 메서드는 지속적으로 살아있으면서 요청이 있을 때마다 실행된다

# Servlet Parmeter
## GET과 POST
이미지추가
- C R U D
- GET에서는 주로 Read
- POST에서는 Create, Update, Delete
- 로그인은 url에 정보가 유출되면 안되므로 post로


## URL 구성요소
이미지추가


### method="GET"
```html
<form action="/gogo" method="GET">
	<!-- name 속성필요. -->
	<input type="text" name="id">
	<input type="password" name="pw">
	<input type="submit">
</form>
```
- id에 "ssafy", pw에 "1234" 입력하고 제출했다면 주소는 다음과 같다
- http://localhost:8080/gogo?id=ssafygr&pw=1234
- url에 정보가 다 보인다


### method="POST"
```html
<form action="gogo" method="POST">
	<!-- name 속성필요. -->
	<input type="text" name="id">
	<input type="password" name="pw">
	<input type="submit">
</form>
```
- id에 "ssafy", pw에 "1234" 입력하고 제출했다면 주소는 다음과 같다
- http://localhost:8080/gogo
- 물론 POST 방식도 개발자모드>Nextwork 에 다 출력된다
- 로그인같은 개인정보는 url에 유출되면 안되므로 post로 설정

### / 유무 차이

- URL에는 IP주소 또는 돈주고 산 도메인이 들어온다
- http://서버/[컨루;컨텍츠 루트]/경로?key=value&key2=value
- ? 다음부터는 처리하기 위한 key와 value가 나온다 
https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query=ssafy

- 프로젝트 파일 우클릭>web context 어쩌구에서 context root를 바꿀 수 있다

- 스프링부트에는 톰캣이 내장되어 있다

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

![서블릿3](https://github.com/namoo1818/TIL/assets/50236187/4cb65d8f-c4fc-49a2-9e7e-9889f1d84303)
![캡처](https://github.com/namoo1818/TIL/assets/50236187/3eec5ca7-e9f8-4e7a-9125-1824a387becc)
![서블릿](https://github.com/namoo1818/TIL/assets/50236187/ffd2d79e-2519-469b-8f08-c71a82d22c21)
![jj](https://github.com/namoo1818/TIL/assets/50236187/fcb0945d-f2f4-44e5-8a32-7816a21b47bd)
![ffd](https://github.com/namoo1818/TIL/assets/50236187/21822c84-f983-467d-8062-7db384886601)
![d](https://github.com/namoo1818/TIL/assets/50236187/74c207a9-365f-47c1-90f9-42288ab307b0)
![서블릿2](https://github.com/namoo1818/TIL/assets/50236187/4b2d9dd3-6349-49ee-ab40-23d3793c0b43)
![action](https://github.com/namoo1818/TIL/assets/50236187/f7112b0f-2d23-46c4-82f5-c243eed528b9)
![url](https://github.com/namoo1818/TIL/assets/50236187/a4f7063a-12e2-4e72-8ef1-0ee38f050220)



