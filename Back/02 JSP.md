### 2023.09.06
# JSP
- Java Server Page
- Servlet 표준을 기반으로 작성된 웹 어플리케이션 개발 언어
- HTML 내에 Java를 작성하여 동적으로 웹페이지를 생성하여 브라우저에게 돌려주는 페이지
- ⭐**실행 시 Servlet으로 변환된 후 실행**
- Servle 내에서 HTML 작성하기 꽤 불편했다 -> Java로 작성하고 HTML에 넣어주자

# 서버 웹페이지 작동 원리
![캡처](https://github.com/namoo1818/TIL/assets/50236187/82e0baa3-5677-47eb-80a1-05f5683d5ab8)
- 클라이언트가 서버에 페이지 요청함
- url이 지정되어 있지 않으면 서버는 파일을 차례대로 읽고 해당 파일이 있다면 응답해줌 

# JSP 동작
![jsp동작](https://github.com/namoo1818/TIL/assets/50236187/97030b49-2125-420d-baa3-4c35ee0280a7)

# JSP 구성요소
![jsp구성요소](https://github.com/namoo1818/TIL/assets/50236187/56aaf0d8-4fab-4692-887a-e3ce141152fc)

# JSP 태그 종류
![jsp기본태그](https://github.com/namoo1818/TIL/assets/50236187/ea00a7d0-ff1d-4f84-836f-5fcb47990182)

## 1. 스크립트릿(Scriptlet)
- 스크립팅 언어(java)로 작성된 코드 조각을 포함하는데 사용
- <% %> 형태
```jsp
<%
  int A = 10;
  int B = 20;
  
  int sum = A + B;
  
  out.print(A+"+"+B+"="+sum);
%>
```
```jsp
10+20=30
```

## 2. 선언부(Declaration)
- 멤버변수 선언이나 메서드를 선언하는 영역
- <%! %> 형태
```jsp
<%!
	// 멤버 변수
	int A = 10;
	int B = -20;
	
	String name = "SSAFY";
	
	// 메서드 선언 가능
	public int add(int A, int B){
		return A + B;
	}
	
	public int abs(int A){
		return A > 0 ? A : -A;
	}
%>
```
```jsp
<%
  out.println(add(A, B));
%><br>
<%
  out.println(abs(B));
%><br>
<%
  out.println(name);
%><br>
```
```jsp
-10
20
SSAFY
```
## 3. 표현식(Expression)
- 변수의 값이나 계산식 혹은 함수를 호출한 결과를 문자열 형태로 웹문서에 출력
- <%= %> 형태
```jsp
<%!
	// 멤버 변수
	int A = 10;
	int B = -20;
	
	String name = "SSAFY";
	
	public int add(int A, int B){
		return A + B;
	}
%>
```
```jsp
<%
  out.println(name);
%>
<%=name %>
<%=A+B %>
<%=add(A,B) %>
```
```jsp
SSAFY
SSAFY
-10
-10
```

## 4. 주석문(Comment)
- HTML 주석문은 클라이언트에게 보여지고, JSP 주석문은 보여지지 않는다.
- HTML 주석 \<!-- -->
- JSP 주석 <%-- -->
```jsp
<!-- 이것은 HTML 주석입니다. (클라이언트에게 노출이 됩니다.) -->
<%-- 이것은 JSP 주석입니다. (클라이언트에게 노출이 되지 않습니다.) --%>
<%
  //이것도 클라이언트에게 노출 안됨
%>
```

# JSP 기본 객체
![jsp기본객체](https://github.com/namoo1818/TIL/assets/50236187/a524040a-c0d2-46b8-a702-f40331ef9cc8)
![jsp기본객체영역메서드](https://github.com/namoo1818/TIL/assets/50236187/30c048f7-8cba-420d-8678-f2e421302320)

# 페이지 이동
### 포워드 방식
![포워드 방식](https://github.com/namoo1818/TIL/assets/50236187/0b28100b-a885-4cfe-9a7a-e8c113de6cfd)
- 서버 내부에서 일어나는 호출
- 한 번 만든 request, response 통로를 계속 사용
```jsp
RequestDispatcher disp = req.getRequestDispatcher("/result.jsp");
disp.forward(req, resp);
```

### 리다이렉트 방식
![리다이렉트 방식](https://github.com/namoo1818/TIL/assets/50236187/ffc44e78-4149-4e1f-bc64-171b30a243ad)
- 여러 서버에서 가능
- 새로운 요청이 들어오면 request, response 통로도 계속 새로 만듦
- 리다이렉트는 특별한 상황에서만 사용
- 입력을 받아 목록에 추가하는 경우 리다이렉트는 통로가 계속 새로 만들어지므로 불가능
```
resp.sendRedirect(req.getContextPath()+"/result.jsp?");
```

# 멤버변수와 지역변수
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%!
	int cnt1 = 0; // 멤버변수
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>호출</title>
</head>
<body>
	<%
  		int cnt2 = 0;
  	
  		out.print(++cnt1); // 새로고침할 때마다 증가
  		out.print("<br>");
  		out.print(++cnt2); // 그대로. service 메서드에 선언된 지역번수라서 실행할 때마다 초기화된다.
	%>
</body>
</html>
```

# 기타

```jsp
<input type="checkbox" id="sleep" name="hobby" value="sleep">
<label for="sleep">수면</label>
```
- for 값은 id 값과 맞춘다

- WEB-INF 폴더는 외부에서 접근 불가
