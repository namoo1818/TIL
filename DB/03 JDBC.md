### 2023.10.12

# JDBC 
- Java DataBase Connectivity
- MySQL로 만든 DB를 Oracle로 변경 또는 Oracle로 만든 DB를 MySQL로 변경할 시 매번 새로 작성해야 했다  
- 매우 불편하니 규격을 만들자! 이것이 JDBC
- Java 프로그램에서 DB에 일관된 방식으로 접근할 수 있도록 API를 제공하는 클래스의 집합
- 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공
- Java에서는 JDBC를 이용하여 SQL을 DMBS와 주고받음
- DBMS 종류와 상관없이 사용 가능(약간의 설정만 조금 수정하면 가능)

# JDBC 이용하여 DB 연결하는 방법 4단계
1. JVM 메모리공간에 JDBC 드라이버 로드
2. 데이터베이스 연결
3. SQL문 실행
4. 데이터베이스 연결 끊음(내가 끄기 전까지 APS는 꺼지지 않으므로)

# JDBC 드라이버 로드
- DB와 연결하기 위해서는 사용할 JDBC 드라이버를 프로그램 시작할 때 로딩
- 필요한 DMBS의 jar 파일을 프로젝트가 추가한다(추가방법 1.직접 jar 추가 2. Maven(pom.xml)에 추가)
- java.lang.Class 클래스의 정적 메소드 forName()을 이용하여 JVM 안으로 클래스를 메모리에 적재
- DriverManager를 통해 접근 가능

# DB별 Driver Class
- MySQL: com.mysql.cj.jdbc.Driver
- Oracle: oracle.driver.OracleDriver
- SQL Server: com.Microsoft.sqlserver.jsdbc.SQLServerDriver

# 데이터베이스 연결
- DriverManager 클래스의 static 메소드인 getConnection(URL, UserId, UserPassword)을 통해 연결 요청
- Connection conn = DriverManager.getConnection("URL","ssafy","ssafy");
- Connection은 인터페이스 이므로 new 연산자를 통해 인스턴스를 생성하지 않고 만들어진 인스턴스를 얻어와 저장한다.(default는 AutoCommit)

# DB별 URL
- MYSQL: jdbc:/mysql://HOST:PORT/DATABASE[?키=값&키=값...]
- HOST는 IP주소, PORT는 포트번호, DATABASE는 DB이름
- 예시: jdbc:mysql://localhost:3306/ssafy_board?serverTimezone=UTC
- Oracle: jdbc:/oracle:thin:@HOST:POST:DATABASE
- SQL Server: jdbc:/sqlserver://[serverName[instanceName][:portNumber]][;property=value...]

# SQL 실행(Statement)
- SQL문을 수행하기 위해서는 Statement 객체가 필요하다
- Connection 객체를 사용하여 createStatement() 메소드를 통해 생성한다
- excuteQuery(String sql): SELECT 문과 같이 결과값이 여러 개의 레코드로 구해지는 경우 사용
- excuteUpdate(String sql): INSERT, UPDATE, DELETE 문과 같이 테이블이 변경만 되고 결과 없는 경우 사용. 반환 값은 int형(변경되는 행의 개수 반환)

# SQL 실행(ResultSet)
- Query에 대한 결과 값 처리
- 반환 값이 여러 개인 경우에 이를 받아서 쉽게 처리할 수 있게 설계됨
- 반환
