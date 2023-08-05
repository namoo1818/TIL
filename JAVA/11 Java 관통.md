### 2023.08.04
# JSON(JavaScript Object Notation)
- 자바스크립트를 토대로 개발
- 여러 프로그래밍 언어에서 사용할 수 있는 독립형 언어
- 웹클라이언트와 웹서버 간 데이터 교환에 사용
- 웹브라우저 비동기 처리에 사용되는 AJAX의 데이터 교환 형식으로 널리 알려짐
- IETF RFC 7159, ECMA-404 표준으로 재정

# JSON을 사용해야 하는 이유
- 주요 프론트엔드 프레임워크에 의해서 지원된다.
- 공식 포맷이기 때문에 개발자 사이에 데이터 통신을 할 수 있다.
- 텍스트로 이루어져 있어 읽고 쓰기 쉽다.
- XML에 비해 용량이 적고 이해하기 쉽다.
- 언어와 플랫폼에 독립적이므로, 서로 다른 시스템간에 데이터 교환에 좋다.

# JSON 구조
- JSON은 key, value의 쌍으로 표현
```
{"key":value, ...}
Key는 ""로 묶어서 표현
Value는 String일 경우 ""로 묶어서 표현
```
- value로 object, array, number, string, true, false, null 사용
- Object 표현
```
{ "id" : "ssafy", "name" : "싸피" }
```
- Array 표현
```
[ "hong", "kim", "park", "lee" ]
```
- 클래스객체와 JSON 변환(type 일치 시)
```
class <-> {}
Array, List <-> []
```

# GSON(Google Gson)
- Java 객체를 JSON 표현으로 변환하는 데 사용할 수 있는 라이브러리다.
- JSON 문자열을 JAVA 객체로, JAVA 객체를 JSON 문자열로 변환하는 간단한 방법을 제공한다. (toJson(), fromJson())
- Gson을 사용하기 위해서 라이브러리를 다운받고 프로젝트에 인식시켜야 한다.
- JavaScript에서는 디폴트로 적용되어 있지만 Java에서 쓰려면 따로 라이브러리를 다운받아야 한다.
```
JSON.stringify() => toJson()
JSON.parse() => fromJson()
```
- GSON 객체 생성
```
Gson gson = new Gson();
```
- 객체 -> JSON 문자열 : gson.toJson()
- JSON 문자열 -> 객체 : gson.fromJson()
