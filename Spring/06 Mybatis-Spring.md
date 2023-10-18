### 2023.10.17

- MyBatis 문서
https://mybatis.org/mybatis-3/ko/getting-started.html

# MyBatis-Spring
- 마이바티스-스프링 연동 모듈은 둘을 간편하게 연동하도록 도와준다
- 해당 모듈은 마이바티스로 하여금 스프링 트랜잭션에 쉽게 연동되도록 처리한다

# MyBatis와 Spring 연동
## 1
- MyBatis와 스프링 프레임워크를 연동하기 위해서는 mybatis-spring 연동 라이브러리가 필요
- jar 파일을 추가하거나 pom.xml을 통해 추가한다
```xml
<!-- MyBatis를 사용하기 위해서 -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.5.9</version>
</dependency>
```

## 2
- MyBatis 실행에 필요한 객체를 root-context.xml에서 Spring Bean으로 등록하여 사용
- dataSource: db 연결 정보, sqlSessionFactory
```xml
<!-- dataSource 가지고와서 빈으로 등록 하자!! -->
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
	<property name="url" value="jdbc:mysql://localhost:3306/ssafy_board?serverTimezone=UTC"/>
	<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
	<property name="username" value="root"/>
	<property name="password" value="ssafy"/>
</bean>
	
<!-- 공장 세워 마이바티스를 사용하기 위해서 sqlSessionFactoryBean 을 등록하자 -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"/>
	<property name="mapperLocations" value="classpath*:mappers/*.xml"/>
	<property name="typeAliasesPackage" value="com.ssafy.board.model.dto"/>
</bean>
```

## 3
- DAO 작성 방법 두가지
1. Mapper 인터페이스를 스프링 빈으로 직접 등록(root-context.xml)
```xml
<bean id="boardDao" class="org.mybatis.spring.mapper.MapperFactoryBean">
	<property name="mapperInterface" value="dao.BoardDao"></property>
	<property name="sqlSessionFactory" ref="sqlSessionFactory"></property>
</bean>
```
2. Mapper scanner를 사용하여 등록(root-context.xml)
- basePackage에 설정된 패키지의 하위의 모든 매퍼 인터페이스가 자동으로 bean으로 등록됨
```xml
<bean id="mapperScanner" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
	<property name="basePackage" value="dao"></property>
</bean>
```

- 통로를 미리 개통하고 요청이 올 때마다 사용한다


# 실습
1. 스프링에서 JDBC가 필요할 때 MVN Repository에서 코드를 가져와서 pom.xml에 복붙한다
```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jdbc</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
```
2. MySQL, MyBatis, MyBatis, MtBatis-Spring, 커넥션도 같은 방법으로 가져온다
```xml
<!-- MySQL 사용하기 위해서... -->
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.21</version>
</dependency>

<!-- MyBatis를 사용하기 위해서 -->
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>3.5.9</version>
</dependency>

<!-- MyBatis 스프링 사용하기 위해서 -->
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis-spring</artifactId>
  <version>2.0.6</version>
</dependency>

<!-- 커넥션을 관리하기 위해서 -->
<dependency>
  <groupId>org.apache.commons</groupId>
  <artifactId>commons-dbcp2</artifactId>
  <version>2.8.0</version>
</dependency>
```
3. 전 프로젝트에서 Board.java, BoardDao.java, BoardService.java를 가져온다
4. BoardService를 implements한 BoardServiceImpl를 만든다
5. bean에 BoardServiceImpl를 등록해야한다 그리고 setBoardDao 메서드 위에 @Autowired를 작성해야 bean에 등록된 게 적용된다 
```spring
@Service
public class BoardServiceImpl implements BoardService {

	private BoardDao boardDao;
	
	@Autowired
	public void setBoardDao(BoardDao boardDao) {
		this.boardDao = boardDao;
	}
...
```
6. root-content.xml에 dataSource를 등록한다
```
<!-- dataSource 가지고와서 빈으로 등록 하자!! -->
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
	<property name="url" value="jdbc:mysql://localhost:3306/ssafy_board?serverTimezone=UTC"/>
	<property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
	<property name="username" value="root"/>
	<property name="password" value="ssafy"/>
</bean>
```
7. 공장을 세워 마이바티스를 사용하기 위해서 sqlSessionFactoryBean을 등록한다
```
<!-- 공장 세워 마이바티스를 사용하기 위해서 sqlSessionFactoryBean 을 등록하자 -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource"/>
	<property name="mapperLocations" value="classpath*:mappers/*.xml"/>
	<property name="typeAliasesPackage" value="com.ssafy.board.model.dto"/>
</bean>
```
8. 마이바티스-스프링에서 제공하는 scan을 통해서 dao 인터페이스 위치를 지정한다(설정 끝)
```
<!-- 마이바티스-스프링 에서 제공하는 scan을 통해서 dao 인터페이스 위치를 지정하겠다!! -->
<mybatis-spring:scan base-package="com.ssafy.board.model.dao"/>
```

# 기타
- test 폴더는 테스트 시 사용하는 폴더로 배포 시 올라가지 않는다
- servlet-context.xml은 웹 관련된 것들을, root-context.xml은 그외의 것들을 관린한다
- 파일 아이콘에 s에 붙어있다면 bean에 등록되어있다는 뜻
- @Component는 @Controller, @Service, @Repository가 있다. 이중에서 @Repository는 마이바티스를 쓰면 사용할 일이 없다. 마이바티스가 인터페이스와 맵퍼 파일을 연동한 구현체를 스프링 설정에 맞춰서 만들어주기 때문이다. 마이바티스 짱!!
