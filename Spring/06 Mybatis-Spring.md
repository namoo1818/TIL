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

```

## 2
- MyBatis 실행에 필요한 객체를 Spring Bean으로 등록하여 사용
- dataSource: db 연결 정보, sqlSessionFactory
```xml

```
```xml

```

## 3
- DAO 작성
- Mapper 인터페이스를 스프링 빈으로 직접 등록
- Mapper scanner를 사용하여 등록
- basePackage에 설정된 패키지의 하위의 모든 매퍼 인터페이스가 자동으로 bean으로 등록됨
```xml

```
```xml

```

- 통로를 미리 개통하고 요청이 올 때마다 사용한다
- SqlSessionFactoryBean을 직접 등록


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
5. bean에 BoardServiceImpl를 등록한다

# 기타
- test 폴더는 테스트 시 사용하는 폴더로 배포 시 올라가지 않는다
- servlet-context.xml은 웹 관련된 것들을, root-context.xml은 그외의 것들을 관린한다
- 파일 아이콘에 s에 붙어있다면 bean에 등록되어있다는 뜻
