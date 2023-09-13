### 2023.09.13
# AOP 관점지향프로그래밍
- OOP(객체지향프로그래밍)에서 모듈화의 핵심 단위는 클래스인 반면, AOP(관점지향프로그래밍)에서 모듈화의 단위는 Aspect
- Aspect는 여러 타입과 객체에 거쳐서 사용되는 기능의 모듈화(Cross Cutting, 트랜잭션 관리 등)
- Cross Cutting: 공통 관심사항이 핵심 관심 사항을 관통하는 느낌
- 핵심기능은 아닌데 여러곳에 들어가는건 따로 만들어서 공통 적용하는게 효율적이다
![aop](https://github.com/namoo1818/TIL/assets/50236187/92a1bd18-d855-4ee7-bb93-123fada3017c)

# 프록시 패턴
<img src="https://github.com/namoo1818/TIL/assets/50236187/a4566126-cd11-4ef3-9c5a-3b91c817da18" href="프록시 패턴" width=500>

# AOP 용어
|용어|내용|
|---|---|
|Aspect|여러 클래스에 공통적으로 구현되는 관심사(Concern)의 모듈화|
|Join Point|메서드 실행이나 예외처리와 같은 프로그램 실행중의 특정 지점. Spring에서는 메서드 실행을 의미한다.|
|Pointcut|Join Point에 Aspect를 적용하기 위한 조건 서술. Aspect는 지정한 pointcut에 일치하는 모든 join point에서 실행된다.|
|Advice|특정 조인포인트(Join Point)에서 Aspect에 의해서 취해진 행동. Around, Before, After 등의 Advie 타입이 존재|
|Target 객체|하나 이상의 advice가 적용될 객체. Spring AOP는 Runtime Proxy를 사용하여 구현되므로 객체는 항상 Proxy 객체가 된다.|
|AOP Proxy|AOP를 구현하기 위해 AOP 프레임워크에 의해 생성된 객체, Spring Framework에서 AOP 프록시는 JDK dynamic 또는 CGLIB proxy이다.|
|Weaving|Aspect를 다른 객체와 연결하여 Advice 객체를 생성. 런타임 또는 로딩 시 수행할 수 있지만 Spring AOP는 런타임에 위빙을 수행|

# Spring AOP Proxy
- 실제 기능이 구현된 Target 객체를 호출하면, target이 호출되는 것이 아니라 advice가 적용된 Proxy 객체가 호출됨
![target호출](https://github.com/namoo1818/TIL/assets/50236187/d18786c6-2691-41f9-9c92-a591cedea3c6)
- Spring AOP는 기본값으로 표준 JDK dynamic proxy를 사용
- 인터페이스를 구현한 클래스가 아닌 경우 CGLIB 프록시를 사용


# Spring AOP
- @AspectJ: 일반 Java 클래스를 Aspect로 선언하는 스타일, AspectJ 프로젝트에 의해 소개되었음
- Spring AOP에서는 pointcut 구문 분석, 매핑을 위해서 AspectJ 라이브러리를 사용함
- 하지만 AOP runtime은 순수 Spring AOP이며, AspectJ에 대한 종속성은 없음

# Spring AOP - xml
## Pointcut 선언

## 

# Spring AOP - Annotation
content가 aop보다 상위 개념

# Advice Type
- before - target 메서드 호출 이전
- after - target 메서드 호출 이후, java exception 문장의 finally와 같이 동작
- after returning - target 메서드 정상 동작 후
- after throwing - target 메서드 에러 발생 후
- around - target 메서드의 실행 시기, 방법, 실행 여부를 결정

# Pointcut Expression 패턴 예시
- (...)은 all를 의미
![패턴 예시](https://github.com/namoo1818/TIL/assets/50236187/6407881c-ffd7-41fa-b2c0-bd7014476805)
