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
1. JDBC 드라이버 로드
2. 데이터베이스 연결
3. SQL문 실행
4. 데이터베이스 연결 끊음(내가 끄기 전까지 APS는 꺼지지 않으므로)

# JDBC 드라이버 로드
- DB와 연결하기 위해서는 사용할 JDBC 드라이버를 프로그램 시작할 때 로딩
- 필요한 DMBS의 jar 파일을 프로젝트가 추가한다(추가방법 1.직접 jar 추가 2. Maven(pom.xml)에 추가)
- java.lang.Class 클래스의 정적 메소드 foorName()을 이용하여 JVM 안으로 클래스를 메모리에 적재
- DriverManager를 통해 접근 가능

# 데이터베이스 연결
- DriverManager 클래스의 static 메소드인

# SQL 실행(Statement)
- int형 반환: 몇개의 데이터를 연결했는지?
