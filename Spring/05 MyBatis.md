### 2023.10.16
# MyBatis
- SQL 매핑 프레임워크
- SQL문과 저장프로시저 등의 매핑을 지원하는 퍼시스턴스 프레임워크(persistence framework)
- JDBC로 처리하는 상당부분의 코드와 파라미터 설정 및 결과 처리를 대신해준다
- Map 인터페이스 그리고 자바 POJO를 설정 데이터베이스와 매핑해서 사용할 수 있다
- XML과 Anootation 설정을 통해 사용할 수 있다

# MyBatis 시작하기
- mybatis-x.x.x.jar 파일을 프로젝트에 추가
- maven 프로젝트를 사용한다면 pom.xml에 의존성 추가

# MyBatis 구성
- 환경설정파일
  - MyBatis 전반에 걸친 세팅
  - DB접속정보, 모델 클래스 정보, 매핑저옵
- Mapper
  - 사용할 SQL문 정의
- Mapped Statment
  - SqlSession 빌드 및 사용
  - SQL문 실행
- Input/Output
  - SQL 실행 시 필요한 데이터
  - SQL 실행결과

# MyBatis 구성
- SqlSessionFactory
  - 모든 마이바티스 애플리케이션은 SqlSessionFactory 인스턴스를 사용한다
  - SqlSessionFactory는 SqlSession을 만든다
- SqlSession
  - 데이터베이스에 대해 SQL 명령어를 실행하기 위한 메서드를 포함한다
- SqlSessionFactory 빌드하기(예시)
```java
String resource = "config/mybatis-config.xml";
Reader reader = Resources.getResourceAsReader(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
```
- SqlSessionFactoryBuilder를 사용하여 SqlSessionFactory 인스턴스를 생성한다

# configuration 작성 순서
 - configuration
   - `properties`
   - settings
   - `typeAliases`
   - typeHandlers
   - objectFactory
   - plugins
   - `environments`(필수작성)
     - environment
       - transactionManager
       - dataSource
    - databaseIdProvider
    - `mappers`(필수작성)
