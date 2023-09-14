### 2023.09.12
# Spring DI
# Spring Framework
![framework1](https://github.com/namoo1818/TIL/assets/50236187/883f5747-50e8-4914-b7be-6fd3c5a0f6de)
![framework2](https://github.com/namoo1818/TIL/assets/50236187/df838bbf-c8fa-4712-a59c-39baa9a20a46)
![framework3](https://github.com/namoo1818/TIL/assets/50236187/eaf3f65c-0d69-4405-b95e-e94c6bb838f2)
- POJO: Java로 생성하는 순수한 객체
- 클래스가 다른 기술에 상속되거나 종속되지 않음
![framework4](https://github.com/namoo1818/TIL/assets/50236187/55fbf4a3-e526-404e-bd63-ba1570d4ea36)
![framework5](https://github.com/namoo1818/TIL/assets/50236187/62cae0e6-d4bd-4a41-a164-83c246396f9e)


# DI란?
- 의존성 주입(Dependency Injection)의 약자
- 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴
- 강하게 결합된 클래스들을 분리
- 애플리케이션 실행 시점에서 객체 간의 관계를 결정
- 결합도를 낮추고 유연성을 확보
- 테스트 작성을 용이하게 함

# 의존관계역전
# 의존성
- ClassA 객체가 어떤 일을 처리하기 위해서 ClassB 객체의 도움을 받아야만 일을 처리할 수 있다면 `ClassA는 ClassB에 의존한다.`고 할 수 있다
- 예를 들어 프로그래머 객체를 생성할 때마다 데스크탑 객체를 안에서 생성해야 한다면 프로그래머 클래스는 데스크탑 클래스에 의존하는 것
## 객체생성 의존성 제거(의존관계 역전)
- 프로그래머 생성할 때마다 컴퓨터를 만들지 말고 만들어진거 쓰겠다
- 스프링이 미리 객체를 만들어놓았다가 필요하면 알아서 조립
- Desktop에 대한 객체생성 의존성이 Programmer->Test로 의존관계가 역전된다(의존성이 제거된다)
## 타입 의존성 제거
### 강한 결합
- 프로그래머에 따라 Laptop, Desktop 선언하기
- 두 클래스가 강하게 결합되어 있음
- 객체들 간의 관계가 아니라 클래스 간의 관계가 맺어짐
### 🌟느슨한 결합
- Computer 인터페이스 하나 만들어서 프로그래머에 선언
- 외부에서 상품을 주입(Injection)받아야 한다
- 코드가 유연해지고 확장성이 있다

# 의존성 주입
## 생성자 이용
```java
public class Programmer {
  private Computer computer;

  // 생성자를 이용한 의존성 주입
  public Programmer(Computer computer) {
    this.computer = computer;
  }

  public void coding() {
    System.out.println(computer.getInfo() + "으로 개발을 합니다.");
  }
}
```
### 설정자 이용
```java
public class Programmer {
  private Computer computer;

  // setter를 이용한 의존성 주입
  public void setComputer(Computer computer) {
    this.computer = computer;
  }

  public void coding() {
    System.out.println(computer.getInfo() + "으로 개발을 합니다.");
  }
}
```
### Factory
```java
public class ComputerFactory {
  public static Computer getComputer(String type) {
    if(type.equals("D"))
      return new Desktop();
    else if(type.equals("L"))
      return new Laptop();
    return null;
  }
}
public class Test {
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    Programmer p = new Programmer();

    Computer computer = ComputerFactory.getComputer(sc.next());
    p.setComputer(computer);
    p.coding();

    Computer computer2 = ComputerFactory.getComputer(sc.next());
    p.setComputer(computer2);
    p.coding();
  }
}
```

# Spring IoC Container
![spring IoC Container](https://github.com/namoo1818/TIL/assets/50236187/dfd66624-7eff-489d-9865-47ef81f1a554)
## 스프링 설정 정보(Spring configuration metadata)
- 애플리케이션 작성을 위해 생성할 Bean과 설정 정보, 의존성 등의 방법을 나타내는 정보
- 설정정보를 작성하는 방법은 XML 방식, Annotation 방식, Java 방식이 있다
![bean scope](https://github.com/namoo1818/TIL/assets/50236187/f943ed50-ef24-48bd-ae99-3f1ca72469ae)

# Spring DI - XML
- ppt 참고

# Spring DI - Annotation
- ppt 참고
