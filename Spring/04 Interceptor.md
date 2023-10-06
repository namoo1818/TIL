### 2023.10.04
# MVC 요청 흐름
![mvc 요청 흐름](https://github.com/namoo1818/TIL/assets/50236187/96bedbcf-4bf3-4b2d-8db0-5a174618a789)

- 스프링에서 모든 요청은 디스패처 서블릿이라는 수문장 하나가 처리함 이를 front-controller라고 함
- 디스패처 서블릿이 제일 먼저 하는 일 : 핸들링(아 이런 요청은 xx 컨트롤러에 가면 되겠다!)
- xx 컨트롤러가 동작함(컨트롤러는 여러개 있을 수 있음)
- bean으로 등록하기 위해 `@Controller`를 활용
- xx 컨트롤러 안에서 메서드를 작성할 수 있음
- 메서드 에는 @RequestMapping @GetMapping @PostMapping같은 것이 붙음
- 게시글 등록, 로그인 등을 하기 위해 xxx servce를 부름
- service는 사용자 친화적으로 되어있고 Dao는 데이터 친화적으로 되어있음
- Dao는 DB와 연결되어 있음(JDBC, Mybatis)
- 이를 담은 객체 바구니를 DTO라고 함
- 메서드의 반환타입은 String(뷰 이름) 또는 Model&View(모델이라는 바구니와 함께 전달)
- Model&View가 디스패처 서블릿에 돌아옴
- 뷰리졸버가 접두사(/WEBINF/views/)와 접미사(.jsp)를 붙여 경로를 완성시킴
- 페이지가 뚜딱뚜딱 만들어지고 이 페이지를 디스패처 서블릿이 클라이언트에게 보냄

![MVC 동작 과정](https://github.com/namoo1818/TIL/assets/50236187/1585ea14-b33e-46cc-95fc-0a5b9d75b0f5)

# Listener
- 프로그래밍에서 Listener란 특정 이벤트가 발생하기를 기다리다가 실행되는 객체
- 이벤트란 특정한 사건 발생
  ex) 버튼 클릭, 키보드 입력, 컨테이너 빌드 완료, 웹어플리케이션 시작, HTTP 요청 수신 등등
- 이벤트 소스란 이벤트가 발생한 근원지(객체)

# Listener 사용(Annotation)
```java
package com.ssafy.mvc;

import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;
import javax.servlet.annotation.WebListener;

@WebListener
public class MyListener implements ServletContextListener {

    public MyListener() {
    }

    public void contextDestroyed(ServletContextEvent sce)  { 
         System.out.println("웹어플리케이션이 종료될 때 호출될 친구");
    }


    public void contextInitialized(ServletContextEvent sce)  { 
    	System.out.println("웹어플리케이션이 시작될 때 호출될 친구");
    }
	
}
```

# Listener 사용(web.xml)
```java
package com.ssafy.mvc;

import javax.servlet.ServletContext;
import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

public class MyListener2 implements ServletContextListener {

    public void contextDestroyed(ServletContextEvent sce)  { 
         System.out.println("웹어플리케이션이 종료될 때 호출될 친구2");
    }

    public void contextInitialized(ServletContextEvent sce)  { 
    	System.out.println("웹어플리케이션이 시작될 때 호출될 친구2");
    	
    	ServletContext context = sce.getServletContext();
    	System.out.println(context.getInitParameter("welcome"));
    }
	
}

```
 
```xml
  <listener>
  	<listener-class>com.ssafy.mvc.MyListener2</listener-class>
  </listener>
  <context-param>
  	<param-name>welcome</param-name>
  	<param-value>Hello SSAFY</param-value>
  </context-param>
```

```
웹어플리케이션이 시작될 때 호출될 친구2
Hello SSAFY
웹어플리케이션이 시작될 때 호출될 친구
```

# Filter
- 요청과 응답 데이터를 필터링하여 제어, 변경하는 역할
- 사용자의 요청이 Servlet에 전달되어지기 전에 Filter를 거침
- Servlet으로부터 응답이 사용자에게 전달되어지기 전에 Filter를 거침
- `FilterChain`을 통해 연쇄적으로 동작 가능
- 어노테이션, xml 모두 가능
![filter](https://github.com/namoo1818/TIL/assets/50236187/a746be31-bb42-44d7-a55b-724c0efd6ad4)

# Filter 사용
```java
package com.ssafy.mvc;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

public class MyFilter implements Filter {

	public FilterConfig filterConfig;
	
    public MyFilter() {
    }

    // 필터 초기화
	public void init(FilterConfig fConfig) throws ServletException {
		filterConfig = fConfig;
	}
    
    // 필터 종료
	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		// 코드를 작성하면
		System.out.println("서블릿 동작 이전에 할 것");
		String encoding = this.filterConfig.getInitParameter("encoding");
		request.setCharacterEncoding(encoding);
//		request.setCharacterEncoding("UTF-8"); // 이런 방식은 유연하지 못함
		chain.doFilter(request, response); // 다음 필터로 전달, 서블릿 호출
		// 코드를 작성하면
		System.out.println("서블릿 동작 이후에 할 것");
	}
}
```

```xml
  <filter>
  	<filter-name>MyFilter</filter-name>
  	<filter-class>com.ssafy.mvc.MyFilter</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  </filter>
  
  <filter-mapping>
  	<filter-name>MyFilter</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
```

```java
package com.ssafy.mvc;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println(request.getCharacterEncoding());
	}
}
```

```
서블릿 동작 이전에 할 것
서블릿 동작 이후에 할 것
서블릿 동작 이전에 할 것
UTF-8
서블릿 동작 이후에 할 것
```

# 필터 추가
- web.xml에 등록된 순서대로 출력된다
```java
package com.ssafy.mvc;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

public class MyFilter2 implements Filter {
	
    public MyFilter2() {
    }

	public void init(FilterConfig fConfig) throws ServletException {
	}
    
    // 필터 종료
	public void destroy() {
	}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		// 코드를 작성하면
		System.out.println("서블릿 동작 이전에 할 것2");
		chain.doFilter(request, response); // 다음 필터로 전달, 서블릿 호출
		// 코드를 작성하면
		System.out.println("서블릿 동작 이후에 할 것2");
	}
}
```

```xml
  <filter>
  	<filter-name>MyFilter</filter-name>
  	<filter-class>com.ssafy.mvc.MyFilter</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  </filter>
  
  <filter-mapping>
  	<filter-name>MyFilter</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
  
    <filter>
  	<filter-name>MyFilter2</filter-name>
  	<filter-class>com.ssafy.mvc.MyFilter2</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  </filter>
  
  <filter-mapping>
  	<filter-name>MyFilter2</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
```

```
서블릿 동작 이전에 할 것
서블릿 동작 이전에 할 것2
서블릿 동작 이후에 할 것2
서블릿 동작 이후에 할 것
서블릿 동작 이전에 할 것
서블릿 동작 이전에 할 것2
UTF-8
서블릿 동작 이후에 할 것2
서블릿 동작 이후에 할 것
```

# Interceptor
- HandlerInterceptor를 구현한 것(또는 HandlerInterceptorAdapter를 상속한 것)
- 요청(requests)을 처리하는 과정에서 요청을 가로채서 처리
- 접근 제어(Auth), 로그(log) 등 비즈니스 로직과 구분되는 반복적으로 부수적인 로직 처리
- 게시글 등록 / 게시글 삭제의 각각의 코드를 만듦
- 두 개의 로직에는 로그인을 했는지 확인하는 과정이 중복되어 들어있음
- 이 때 접근 제어나 로그를 활용

# HandlerIntercepter의 주요 메서드
## preHandle()
- boolean 타입 반환
- 디스패처 서블릿에서 컨트롤러로 요청을 보낼 때 가로채서 확인
- false를 반환하면 요청을 종료한다
- true면 그냥 계속 진행해

## postHandle()
- 컨트롤러 실행 후 호출
- 컨트롤러가 디스패처 서블릿한테 Model&View를 전달하기 때문에 매개변수에 M&V가 있음
- 정상 실행 후 추가 기능 구현 시 사용
- 컨트롤러에서 예외 발생 시 해당 메서드는 실행되지 않는다

## afterCompletion()
- 뷰가 클라이언트에게 응답을 전송한 뒤 실행
- 컨트롤러에서 예외 발생 시, 네번째 파라미터로 전달됨(기본은 null)
- 따라서 컨트롤러에서 발생한 예외 혹은 실행 시간 같은 것들을 기록하는 등 후처리 시 주로 사용

# Interceptor 흐름
![interceptor 흐름](https://github.com/namoo1818/TIL/assets/50236187/58eeca76-48db-4d00-98f1-4457a4d12d21)


- servlet-context : 웹과 관련된 설정이 들어있다
- root-context : 웹 이외의 설정이 들어있다  

AInterceptor, BInterceptor, CInterceptor를 차례대로 servlet-context.xml에 등록할 경우

```
A : preHandle
B : preHandle
C : preHandle
C : postHandle
B : postHandle
A : postHandle
C : afterCompletion
B : afterCompletion
A : afterCompletion
```

- \<a href="regist">게시글 등록</a>
- 마지막 / 다음으로 regist가 붙음
- http://localhost:8080/mvc/regist
