### 2023.08.02
# 자바스크립트란?
- 프로토타입 기반 객체 생성을 지원하는 동적 스크립트 언어
- 웹 브라우저에서 주로 사용, Node.js를 이용하여 콘솔 환경에서 사용
- 웹 브라우저의 UI를 제어하기 위해 만들어진 프로그래밍 언어
- 자바와 기본 구문이 비슷하다. (C언어의 기본 구문을 바탕)
- 브랜든 아이크 개발(1995)
- Mocha -> LiveScript -> JavaScript

### 자바스크립트는 인터프리터 언어다.
- 인터프리터 언어 : 소스코드를 한 줄 한 줄 읽어가며 명령을 바로 처리하는 프로그래밍 언어. 번역과 실행이 동시에 이뤄진다.
> 자바스크립트, 파이썬, 루비, sql, ...
- 컴파일 언어 : 소스코드를 한꺼번에 다른 목적 코드로 번역한 후, 한 번에 실행하는 프로그래밍 언어
> C, C++, C#, Go,...

## 호이스팅(hoisting)
인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것

# 기본 문법
## 1. HTML 자바스크립트 사용
- \<script></script> 태그를 사용
- **문서 내의 위치의 제약이 없다.**

## 2. 외부스크립트 참조하기
- .js 확장자를 가진 파일을 생성
- html 문서에서 <script src="외부파일의 위치">\</scropt>

## 3. 주석(Comment)
- // 한 줄 주석
- /**/ 여러 줄 주석

## 🌟4. 변수(Variable)
- 자바스크립트의 변수 타입은 가리키는 값에 대한 타입을 나타낸다.
- var, let, const 키워드를 이용해서 변수를 선언
- var를 이용한 변수의 선언일 경우 중복 선언이 가능
- undefined 는 변수에 아무 값도 없어서 타입을 알 수 없는 경우를 말한다.
- 동적 타입 : 대입되는 값에 따라서 용도가 변경되는 방식
- 문자, $, _로 시작, 대소문자 구분, 예약어 사용 x

### var
- 재 선언 가능, 재 할당 가능
- ES6 이전에 변수 선언 시 사용
- **호이스팅(Hoisting) 특성이 있다.**
- 함수 스코프

### let
- 재 선언 불가, 재 할당 가능
- 블록 스코프

## const
- 재 선언 불가, 재 할당 불가
- 블록 스코프
- 대문자 SNAKE_CASE 사용
- 선언 시 값을 할당해야 함
- 상수로 사용

## ⭐undefined
- 변수에 값이 대입되지 않은 상태

## 함수 스코프 vs 블록 스코프
### 스코프(scope)
> 변수에 접근할 수 있는 범위. 함수가 선언되면 생성.
### 컨텍스트(context)
> 함수가 속해있는 객체가 무엇인지 의미.
### 함수 스코프
- 새로운 함수가 생성될 때마다 새로운 스코프 발생
- 자바스크립트는 기본적으로 함수 스코프를 따르는 언어
- ex) var
### 블록 스코프
- 블록{}이 생성될 때마다 새로운 스코프 발생
- ex) let, const

참고 : https://velog.io/@fromzoo/%ED%95%A8%EC%88%98%EC%8A%A4%EC%BD%94%ED%94%84-vs-%EB%B8%94%EB%A1%9D%EC%8A%A4%EC%BD%94%ED%94%84

# 데이터 타입 (Data Type)
### 기본 데이터 타입 (Primitive Type)
> String, Number, Boolean, null, undefined
- null: 값을 일부러 비울 때
- undefined: 선언만 하고 할당하지 않았을 때
### 객체 타입 (Reference Type)
> Object - function, array 등
- 주소 저장
### Symbol(esb 추가)
변경 불가능한 기본타입
- 유일무이한 값

# typeof - 변수의 자료형 검사
- typeof 데이터
- typeif (데이터)
- typeof 의 결과는 문자열 반환
- null의 데이터 타입은 null이 아닌 object(설계 실수)
- function 은 기능을 가진 객체

```javascript
let num1 = 10; 
let num2 = 10.2;
let msg = "hi";
let bool = true; 
let nullVal = null; 
let unVal; 
let obj = {}; 
let obj2 = new Object(); 
let symbol = Symbol();

// 데이터 타입의 확인에는 typeof 연산자 사용
console.log(typeof num1); // numer
console.log(typeof num2); // numer
console.log(typeof msg); // string
console.log(typeof bool); boolean
console.log(typeof nullVal); // null -> object 
console.log(typeof unVal); // undefined -> undefined 
console.log(typeof obj); // object
console.log(typeof obj2); // object
console.log(typeof symbol); // symbol
```

# 동적 데이터 타입 - 다양한 값의 대입이 가능
```javascript
var val = 10;
console.log(val, typeof(val)); // 10 'number'
val = "hello";
console.log(val, typeof(val)); // hello string
val = true;
console.log(val, typeof(val)); // true 'boolean'
```

# 숫자형(Number)
- 정수와 실수로 나누어 구분하지 않음>(부동소수점 형식)
- 일반적인 숫자 외 특수 숫자 포함(Infinity, Nan...)
- e를 활용하여 거듭제곱 표현 가능
```javascript
let x = 0.3 - 0.2;
let y = 0.2 - 0.1;
console.log(x == y); // false
console.log(x); // 0.09999999999999998
console.log(y); // 0.1
```
# 문자열(String)
- ""로 감싼다.
- ''로 감싼다.
- ``(backtick)으로 감싼다. -> Template Literal(ES6)
> 여러 줄 입력이 가능 - 공백, 줄 넘김 유지  
> 문자열 내 ${변수명}을 이용하여 변수와 문자열을 결합
- UTF-16 방식
```javascript
let name = "홍길동";
let age = 33;

let msg1 = "이름은 "+name+ ", 나이는 " +age+ " 입니다.";
let msg2 = `이름은 ${name}, 나이는 ${age} 입니다.`;
console.log(msg1);
console.log(msg2);
```
```
이름은 홍길동, 나이는 33 입니다.
이름은 홍길동, 나이는 33 입니다.
```
# 문자열(String) 연산
- 문자열과 숫자 타입의 + 연산 -> 문자열
- 문자열과 숫자 타입의 + 연산 -> 숫자
```javascript
// 문자열 취급
console.log(1 + "20"); // 120
console.log("1" + "20"); // 120
console.log("1" + 20); // 120
// 숫자 취급
console.log("100" - 8); // 92
console.log("100" * 8); // 800
```
# 자바스크립트 false
- false로 인식 : null, undefined, 0, ''(빈문자열), Nan
- true로 인식 : 그 외 나머지
```javascript
console.log(!!0); // false
console.log(!!""); // false
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!NaN); // false
console.log(!!"0"); // 비어있지 않은 문자열 true
console.log(!!Number("0")); // false
console.log(Boolean()); // false

let id;
console.log(id);
if (id) {
  console.log("id 값이 있는 경우.");
} else {
  console.log("id 값이 없는 경우");
}
```
# 연산자(Operator)
**(거듭제곱) 제외하면 자바와 동일

# 🌟일치 연산자
- 값과 타입이 일치하는지 체크
- ===, !==
```javascript
var i = 100;
var j = "100";

console.log(

```
# 제어문(Java와 유사)
- 조건문(Condition)
> - if
> - switch
- 반복문(Loop)
> - for
> - while
> - do-while

# 배열(Array)
- 배열의 생성 : [] 또는 Array() 활용
- 배열의 크기는 동적으로 변경된다.
- 크기가 지정되어 있지 않은 경우에도 데이터의 입력 가능
- 배열의 길이는 가장 큰 인덱스 + 1한 값이다.
- 배열은 여러가지의 데이터 타입을 하나의 배열에 입력할 수 있다.
- push 함수를 이용하여 데이터 추가 가능
```javascript
var arr1 = []
var arr2 = new Array();

arr1[0] = 10;
arr2[2] = 30;
console.log(arr1[0], arr1[1], arr1[2]); // 10 undefined 30
console.log(arr1.length); // 3

arr1[3] = "문자열";
arr1[4] = {};
arr1[5] = [1,2,3];
arr1[6] = true;
arr1.push("추가");
```

# 객체(Object)
- 객체는 문자열로 이름을 붙인 값들의 집합체이다 (Key : Value)
- 객체에 저장하는 값을 프로퍼티(Property)라고 한다.
- 객체는 prototype이라는 특별한 프로퍼티를 가지고 있다.

## 객체(Object) 만들기
- 객체 리터럴 이용 : {}
- Object 생성자 이용 : new Object()
- 생성자 함수 이용
```javascript
let member1 = {}
let member2 = new Object();
function Member(){}
let member3 = new Member()
```

## 객체(Object) 생성 시 프로퍼티 추가
```javascript
let member1 = {id: "shy", email: "ssafy@a.com"}
function Member(id, email) {
  this.id = id;
  this.email = email;
}
let member2 = new Member("shy", "ssafy@a.com");
```
## 객체(Object) 프로퍼티
- .(dot) 또는 []를 아용하여 프로퍼티의 조회 및 변경을 처리한다.
```javascript
let student = {
  name: "김싸피",
  age: 20,
  hobby: ["공부", "숙면"],
  "favorite singer":"아이유",
};

console.log(student.name);
console.log(student[age]); // 에러
console.log(student.hobby);
console.log(student["favorite singer"]);
```
```javascript
var member = {};
member ["id"] = "ssafy";
member.name = "싸피";
```
## 객체(Object) 프로퍼티 - 추가 / 수정 / 삭제
- 추가
```javascript
var member = {"id":"hong","email":"hong@a.com"};

// 동적인 프로퍼티 추가
member.name = "홍길동";
console.log(member);
```
- 수정
```javascript
let member = {id: "shy", email: "ssafy@a.com"}
member["id"] = "ssafy";
member.email = "ssafy@ssafy.com";
```
- 삭제
```javascript
let member = {id: "shy", email: "ssafy@a.com"};
delete member.id;
console.log(member);
```
## 객체 변수에는 주소가 저장되어 공유 가능
```javascript
let member1 = {id: "hong", email: "hong@a.com"}
let member2 = member1;
member2.id = "kang";

console.log(member1.id); // kang
console.log(member2.id); // kang
```
# 🌟함수안에서의 this는 함수를 호출한 객체
```javascript
var m1 = {name: "홍길동"};
var m2 = {name: "배수지"};
function msg() {
  console.log(this);
  console.log(this.name + "님이 입장함");
}
m1.msg = msg;
m2.msg = msg;
m1.msg();
m2.msg();
```
# 함수 특징
- 자바스크립트에서 함수는 객체 타입으로 값처럼 사용이 가능하다.
- 함수를 변수에 대입하거나 매개변수로 넘길 수 있다.
- 배열의 요소에 넣거나 객체의 프로퍼티로 설정이 가능하다.
- 매개변수의 개수가 일치하지 않아도 호출이 가능하다.
- JavaScript의 함수는 일급 객체(First-class citizen)에 해당
> - 변수에 할당 가능
> - 함수의 매개변수로 전달 가능
> - 함수의 반환 값으로 사용가능
## 함수 만들기
- 함수 선언식 function함수명() {함수 내용}
- 함수 표현식 let 함수명 = function() {함수 내용}
## 함수 선언식(function declaration)
- 함수의 이름과 함께 정의하는 방식
- 함수의 이름
- 매개 변수
- 내용
- ⭐호이스팅 됨 (아까 var도 호이스팅 되었음)
## 함수 표현식(function expression)
- 익명함수로 정의가능
- 매개 변수
- 내용
- 호이스팅 안됨

## 선언식 vs 표현식
- 선언식 함수는 호이스팅의 영향을 받아 함수 선언 이전에 호출이 가능하다.
- 표현식 함수는 선언 이전에 호출이 불가능하다.
```javascript
// 선언식 : 호출 가능
func();
function func() {
  console.log('선언식');
}
```
```javascript
// 표현식 : 호출 불가능
func();
let funct = function() {
  console.log('표현식');
};
```
## 함수의 리턴
- 함수의 실행 결과로 함수를 반환할 수 있다.
- 함수가 특별한 값을 리턴하지 않은 경우 undefined가 반환된다.
```javascript
function func() {
  return function (num1, num2) {
    return num1 + num2;
  };
}

function func2() {}

console.log(func()(100, 200)); // 300
console.log(func2()); // undefined
console.log(func()(100)); // NaN
```
## 함수의 호출
- 정의된 함수를 호출 시 함수를 값으로 넘길 수 있다.
```javascript
function func(callFn) {
  callFn('hello');
}
function fn(msg) {
  console.log(msg);
}
```
```javascript
func(fn); // hello 출력
```
## 함수 매개변수
- 함수는 호출 시 매개변수의 영향을 받지 않는다.
- arguments라는 함수 내부의 프로퍼티를 이용하여 매개변수의 처리가 가능하다.
- **자바스크립트의 함수는 오버로딩 개념을 지원하지 않는다.**
- 기본 인자(default arguments)를 사용할 수 있다.
```javascript
// 1
function fn1(num) {
  console.log("fn1", num)
}
```
```javascript
fn1(); // undefined
fn1(100); // 100
fn1(100, 100); // 두개의 arguments 중 앞에 하나만 처리 
```

```javascript
// 2
function fn() {
  console.log(arguments.length);
  for (let i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}
```
```javascript
// 출력 결과
fn(1);
1
1
fn(1, 10, 100);
3
1
10
100
```
```javascript
// 3
function fn() {
  console.log(1);
}
function fn() {
  console.log(2);
}
function fn(num) {
  console.log(num);
}
```
```javascript
fn(); // undefined, 오버로딩 지원 x
fn(1); //1
```

# JavaScript 공부 사이트
https://www.w3schools.com/  
https://ko.javascript.info/

