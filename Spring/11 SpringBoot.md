# SpringBoot
- Spring Framework 경량화 버전
- XML 기반의 복잡한 설계 방식을 사용하지 않는다.
- 의존 라이브러리를 자동으로 관리해 준다.
- 애플리케이션 설정을 자동으로 구성한다.
- 프로덕션(Production) 애플리케이션을 쉽게 빌드할 수 있다.
- 내장된 WAS(톰캣)를 통해 보다 쉽게 배포할 수 있다.
- context path는 없다, 1플젝 1톰캣이라 구별할 필요가 없어서.
- Lombok: getter&setter를 annotation으로 넣어준다. 같이 개발하는 사람은 같은 Lombok 환경이 갖춰져야 한다


# SpringBoot Project 구조(STS)
![sts](https://github.com/namoo1818/TIL/assets/50236187/b537abec-8dd3-4351-b00e-b47a2c469745)


# 실습
- new starter project 생성
- https://start.spring.io
- uri에서 '?' 다음은 쿼리 String

## application.properties
- spring 설정 파일(servlet-context.xml, root-context.xml)은 필요없다
```java
# JSP path
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp

# dataSource
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/ssafy_board?serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=ssafy

# mybatis
mybatis.mapper-locations=classpath*:mappers/*.xml
mybatis.type-aliases-package=com.ssafy.board.model.dto
```

## DBConfig.java
```java
package com.ssafy.board.config;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@MapperScan(basePackages = "com.ssafy.board.model.dao")
public class DBConfig {

}
```

## WebConfig.java
```java
package com.ssafy.board.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.ViewResolver;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
import org.springframework.web.servlet.view.InternalResourceViewResolver;
import org.springframework.web.servlet.view.JstlView;

@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
	@Value("${spring.mvc.view.prefix}")
	private String prefix;
	@Value("${spring.mvc.view.suffix}")
	private String suffix;

	// 추후에 관심이 있다면 FileDownload도 처리해보자.
	@Bean
	public ViewResolver internalResourceViewResolver() {
		InternalResourceViewResolver resolver = new InternalResourceViewResolver();
		resolver.setPrefix(prefix);
		resolver.setSuffix(suffix);
		resolver.setViewClass(JstlView.class);
		return resolver;
	}

	@Override
	public void addResourceHandlers(ResourceHandlerRegistry registry) {
		registry.addResourceHandler("/**").addResourceLocations("classpath:/static/");
	}
	
	//등록할 인터셉터가 있다면... 
	//필드를 통해 의존성을 주입 받고
	@Override
	public void addInterceptors(InterceptorRegistry registry) {
		//등록하면된다...
	}
}
```

## loginform.jsp
- context root가 없어졌기 때문에 /login으로 경로를 변경해도 된다.
```jsp
<form action="/login" method="POST">
```
