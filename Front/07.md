### 2023.10.26

# ES6(ECMAScript 6)
- ECMAScript는 ECMA-262 기술 규격에 정의된 표준화된 스크립트 프로그래밍 언어
- JavaScript 언어 등을 표준화하기 위해 만들어짐
- ES5(2009) -> ES6(2015): 많은 문법적 요소들이 추가

# 화살표 함수(Arrow Function)
- 함수를 심플하게 정의할 수 있도록 해준다
- 형태: (매개변수)=>{명령어}
- **주의사항**           
  > 기존의 함수에서 사용하는 this와 화살표 함수의 this는 서로 다른 this 값이 바인딩(연결)될 수 있다.       
  > 기존함수의 this는 메서드가 호출 될때마다 현재 호출중인 메서드를 보유한 객체가 this로 연결     
  > 현재 호출중인 메서드를 보유한 객체가 없다면 전역 객체 (브라우저 환경에서의 window 객체)가 연결     
  > 화살표 함수는 함수가 정의되는 유효 범위의 this를 자신의 유효범위 this로 연결      
```javascript
let add = function (a, b) {
  return a + b;
};
let add2 = (a, b) => {
  return a + b;
};
let add3 = (a, b) => a + b;
```

# 기본 파라미터(Default Parameter)
- 함수 파라미터의 기본값을 지정할 수 있다
- 기본 인자를 쓰지 않으면 undefined가 된다
```javascript
function myInfo(name, age = 0, address = "x", email = "x") {
  console.log(
    `이름 : ${name}, 나이 : ${age}, 주소 : ${address}, email=${email}`
  );
}
```

# 가변 파라미터(Rest Parameter)
- 여러 개의 파라미터 값을 배열로 받을 수 있음
```javascript
function myInfo(name, age, ...hobbies) {
  console.log(`이름 : ${name}, 나이 : ${age}`);
  console.log(hobbies);
}

myInfo("양띵균", 42, "공부", "수면", "식사");
myInfo("양띵균2", 42, "공부", "수면");
```
```
이름 : 양띵균, 나이 : 42
(3) ['공부', '수면', '식사']
이름 : 양띵균2, 나이 : 42
(2) ['공부', '수면']
```

# ⭐구조분해 할당(Destructuring Assignment)
-배열, 객체의 값들을 추출하여 한번에 여러 변수에 할당할 수 있음
```javascript
let user = {
    id: "ssafy",
    name: "양띵균",
    age: 22,
};

let { id, name, age } = user;
console.log(`${id}님의 이름은 ${name} 이고, 나이는 ${age}살 입니다.`);
```
```
ssafy님의 이름은 양띵균 이고, 나이는 22살 입니다.
```
```javascript
//ES6 전
function showMember(member) {
    console.log("showMember1");
    console.log("아이디 :", member.id);
    console.log("이름 :", member.name);
    console.log("나이 :", member.age);
}
//ES6 후
function showMember2({ id, name, age }) {
    console.log("showMember2");
    console.log("아이디 :", id);
    console.log("이름 :", name);
    console.log("나이 :", age);
}
```

# 객체 속성 표기법 개선
- shorthand properties
- concise method
```javascript
const id = "ssafy";
const name = "싸피";
const age = 3;

// ES5
const member1 = {
    id: id,
    name: name,
    age: age,
    info: function () {
        console.log("info");
    },
};

// ES6
const member2 = {
    id,
    name,
    age,
    info() {
        console.log("info");
    },
};
```

# 모듈(Module)
- 독립성을 가진 재사용 가능한 코드 블록
- 여러 개의 코드 블록을 각각의 파일로 분리한 후 필요한 모듈을 조합하여 사용 가능
- import/export 구문을 이용하여 가져오거나 내보낼 수 있음
- module1
```javascript
const title = "계산기 모듈";

function add(i, j) {
  return i + j;
}

function sub(i, j) {
  return i - j;
}

export { title, add, sub };
```
- module2
```javascript
export default {
  title: "계산기 모듈",
  add(i, j) {
    return i + j;
  },
  sub(i, j) {
    return i - j;
  },
};
```
```javascript
import { title, add, sub } from "./08_module1.js";
import calc from "./08_module2.js";

console.log(title);

document.querySelector("#calc").addEventListener("click", () => {
    // +가 없으면 String으로 인식
    let num1 = +document.querySelector("#num1").value;
    let num2 = +document.querySelector("#num2").value;

    //모듈1
    console.log(add(num1, num2));
    console.log(sub(num1, num2));

    //모듈2
    console.log(calc.add(num1, num2));
    console.log(calc.sub(num1, num2));
});
```

# 전개 연산자(Spread Operator)
- 가변 파라미터와 동일한 기호 ... 사용
- 배열이나 객체를 연산자와 함께 객체 리터럴, 배열 리터럴에서 사용하면 객체, 배열 내의 값을 분해된 형태로 전달
- 깊은 복사 수행 시 자주 사용

```javascript
let user1 = {
    id: "ssafy",
    name: "양띵균",
    age: 40,
};

let user2 = user1; // 얕은 복사

let user3 = { ...user1 }; // 깊은 복사

user2.age = 50;
console.log(user1);
console.log(user2); // 나이 50
console.log(user3); // 나이 40
console.log(user1 == user2); // true
console.log(user1 == user3); // false

/////
let arr1 = [1, 2, 3, 4];
let arr2 = [100, ...arr1, 200];

console.log(arr1); // [1,2,3,4]
console.log(arr2); // [100,1,2,3,4,100]
```

# 순차적인 비동기 처리하기
- Web API로 들어오는 순서는 중요하지 않고, 어떤 이벤트가 먼저 처리되느냐가 중요.(실행 순서 불명확)

1. Async Callbacks
   - 백그라운드에서 실행을 시작할 함수를 호출할 때 인자로 지정
   - ex) addEventListener()의 두번째 인자
2. Promise-Style
   - Modern Web APIs에서의 새로운 코드 스타일
   - XMLHttpRequest 객체를 사용하는 구조보다 조금 더 현대적인 버전

# 콜백(Callback)이란?
- 함수를 매개변수로 전달하여, 나중에 실행하도록 하는 것
- 콜백이 중첩되면, 콜백 헬이 되어 해석하고 유지보수하기 힘든 코드가 될 우려(스파게티 코드)
```javascript
let work = true; // 임시

function task(successCallback, failureCallback) {
    // 어떠한 작업을 통해 work라고 하는게 성공/실패를 할 것이다.
    if (work) {
        successCallback();
    } else {
        failureCallback();
    }
}

function onTaskSuccess() {
    console.log("작업이 성공하면 이 콜백함수를 실행합니다.");
}

function onTaskFailure() {
    console.log("작업이 실패하면 이 콜백함수를 실행합니다.");
}

task(onTaskSuccess, onTaskFailure);

// 이런 것도 가능
task(
    () => {
        console.log("작업이 성공하면 이 콜백함수를 실행합니다.");
    },
    () => {
        console.log("작업이 실패하면 이 콜백함수를 실행합니다.");
    }
);
```
- 아래 코드처럼 중첩도 가능
```javascript
function task(successCallback, failureCallback) {
  if (work1) {
    successCallback();
  } else {
    failureCallback();
  }
}

function onTask1Success(successCallback, failureCallback) {
  console.log("work1 작업이 성공했습니다.");
  if (work2) {
    successCallback();
  } else {
    failureCallback();
  }
}

function onTask1Failure() {
  console.log("work1 작업이 실패했습니다.");
}

function onTask2Success() {
  console.log("work2 작업이 성공했습니다");
}

function onTask2Failure() {
  console.log("work2 작업이 실패했습니다");
}

task(() => onTask1Success(onTask2Success, onTask2Failure), onTask1Failure);
```

# Promise Object
- 위에 너무 극혐임 promise로 예쁘게 만들자
- **비동기 작업을 마치 동기 작업처럼 값을 반환해서 사용 형태**
- 미래의 완료 또는 실패와 그 결과 값을 나타냄
- 미래의 어떤 상황에 대한 약속
- 변수를 만드는 순간 Promise 객체가 생성됨. `let TaskPromise = new Promise();`
- new Promise(function(resolve, reject){})
- resolve(성공 시 사용)
- reject(실패 시 사용)
```javascript
const p = new Promise((resolve, reject) => {
    console.log("p 작업이 수행 중입니다.");
    let task = true;
    if (task === true) {
        resolve("p 작업이 성공했습니다.");
    } else {
        reject("p 작업이 실패했습니다.");
    }
});

p.then((response) => {
    console.log(`p 프라미스가 resolve됨: ${response}`);
}).catch((response) => {
    console.log(`p 프라미스가 reject됨: ${response}`);
});
```
```
p 작업이 수행 중입니다.
p 프라미스가 resolve됨: p 작업이 성공했습니다.
```

# Promise Methods
### .then(callback)
- Promise 객체를 리턴하고 두 개의 콜백 함수를 인수로 받는다.(이행했을 때, 거부했을 때)
- 콜백 함수는 이전 작업의 성공 결과를 인자로 전달 받음
### .catch(callback)
- .then이 하나라도 실패하면(거부되면) 동작(예외 처리 구문 유사)
- 이전 작업의 실패로 인해 생성된 error 객체는 catch 블록 안에서 사용 가능
### .finally(callback)
- Promise 객체 반환
- 결과 상관없이 무조건 실행
```javascript
let task1 = false;
let task2 = false;

function task1Promise() {
  return new Promise((resolve, reject) => {
    if (task1) {
      resolve("task1이 성공했습니다.");
    } else {
      reject("task1이 실패했습니다");
    }
  });
}

function task2Promise() {
  return new Promise((resolve, reject) => {
    if (task2) {
      resolve("task2가 성공했습니다.");
    } else {
      reject("task2가 실패했습니다.");
    }
  });
}

task1Promise()
  .then((response) => {
    console.log(response);
    return task2Promise();
  })
  .then((response) => {
    console.log(response);
  })
  .catch((response) => console.log(response));
```
```
task1이 실패했습니다
```
### 체이닝 가능
```javascript
function TaskHasDuration(duration) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            // 이 작업을
            resolve(duration);
        }, duration); // duration 경과하면 수행
    });
}

// sync
// 체이닝해서 동기방식으로도 사용할 수가 있다.
TaskHasDuration(3000)
  .then((message) => {
    console.log(message);
    return TaskHasDuration(3001);
  })
  .then((message) => {
    console.log(message);
  });
```
```
3000
3001
```
- Promise.all(): 서로 다른 사이트에서 의존성 없는 것들을 모아 한방에 처리
```javascript
Promise.all([
  TaskHasDuration(1000), // task 1
  TaskHasDuration(2000), // task 2
  TaskHasDuration(3000), // task 3
  TaskHasDuration(4000), // task 4
  TaskHasDuration(5000), // task 5
]).then((messages) => {
  // task 1, 2, 3, 4, 5에 모두 의존하는 작업을
  // 여기서 수행
  console.log(messages);
});
```
```
(5) [1000,2000,3000,4000,5000]
```
- Promise.race(): 여러 작업 들 중 가장 먼저 완료된 작업을 반환
```javascript
Promise.race([
    TaskHasDuration(1000), // task 1
    TaskHasDuration(2000), // task 2
    TaskHasDuration(3000), // task 3
    TaskHasDuration(4000), // task 4
    TaskHasDuration(5000), // task 5
]).then((message) => {
    // 5개 중에 가장 빠른애 하나만!
    // 선택지가 여러개가 있을 때
    // 똑같은 기능을 하는 서버가 5개
    //
    // task 1, 2, 3, 4, 5 중 하나만 필요한 작업을
    // 여기서 수행
    console.log(message);
});
```
```
1000
```

# fetch API
- XMLHttpRequest보다 강력하고 유연한 조작이 가능
- Promise를 지원하므로 콜백 패턴에서 자유로움
- ES6문법은 아니고, BOM(Brower Object Model) 객체 중 하나
- fetch() 메서드는 HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환

# fetch(resource, options) 메서드
- resource: 리소스가 위치한 url 지정
- options: 옵션을 지정
  - method: HTTP method
  - headers: 요청 헤더 지정
  - body: 요청 본문 지정
- fetch 메서드는 Promise 객체를 반환

# fetch()가 반환하는 Promise 객체
- 성공시 then()을 이용해 처리
- 실패시 catch()를 이용해 처리

# fetch 사용 예
- fetch 메서드는 HTTP 응답을 나타내는 Response 객체를 래핑한 Promise 객체를 반환
- **response.text()**: Response의 Body를 텍스트의 형태로 반환
- **response.json()**: Response의 Body를 JSON 파싱하여 반환

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>fetch</title>
    </head>
    <body>
        <script>
            fetch("https://jsonplaceholder.typicode.com/posts/1")
                .then((response) => response.text())
                .then((text) => JSON.parse(text).body)
                .then((body) => console.log(body));
        </script>
    </body>
</html>
```
```
quia et suscipit
suscipit recusandae consequuntur expedita et cum
reprehenderit molestiae ut ut quas totam
nostrum rerum est autem sunt rem eveniet architecto
```
- fetch 오류 메세지
- finally는 무조건 실행된다
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>fetch</title>
  </head>
  <body>
    <script>
      fetch("http://somewrongurl....")
        .then(() => console.log("ok"))
        .catch((e) => console.log(e))
        .finally(()=> {
          console.log("무조건실행")
        })
    </script>
  </body>
</html>
```
![오류](https://github.com/namoo1818/TIL/assets/50236187/91a02555-bee6-4095-b3d1-47cf3b58681e)
- 어제 했던 XMLHttpRequest 코드를 fetch로 구현해보자
![xml과 fetch](https://github.com/namoo1818/TIL/assets/50236187/ee999232-9ca1-4510-96e9-66078766a6cf)
![ajax](https://github.com/namoo1818/TIL/assets/50236187/3826028c-0d31-414f-90ad-f438e6bdf3bb)
