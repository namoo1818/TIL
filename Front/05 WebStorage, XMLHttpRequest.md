# Web Storage API
- 키/값 쌍으로 값을 저장
## sessionStorage
- 각각의 출처에 대해 독립적인 저장 공간을 페이지 세션이 유지되는 동안(브라우저가 열려있는 동안) 제공.
- 세션에 한정해, 즉 브라우저 또는 탭이 닫힐 때까지만 데이터를 저장.
- 데이터를 절대로 서버로 전송하지 않는다.
- 저장 공간이 쿠키보다 크다.(최대 5MB)
## localStorage
- localStorage도 위와 같지만, 브라우저를 닫았다 열어도 데이터가 남아있다.
- 유효기간 없이 데이터를 저장하고, JavaScript를 사용하거나 브라우저 캐시 또는 로컬 저장 데이터를 지워야만 사라진다.
- 저장공간이 가장 크다.

https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API

# Storage
- 속성
  - length: 객체에 저장된 데이터 항목의 수를 반환
- 메서드
  - key(index): index번째의 키를 반환
  - getItemm(key): keyt에 해당하는 값 반환
  - setItem(key, value): key가 존재하는 경우 재설정, 존재하지 않는 경우 추가
  - removeItem(key): key를 저장소에서 제거
  - clear(): 모든 키를 저장소에서 제거

# 실습
- addEventListener(행위, 콜백함수)
- JS에서 함수는 일급객체라서 변수에 할당하거나 다른 함수를 인자로 받을 수 있다.
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>로컬스토리지 실습</title>
    </head>
    <body>
        <h1>로컬스토리지</h1>
        <input type="text" id="input" placeholder="내용을 입력해보자." />
        <button id="create">등록</button>
        <button id="read">조회</button>
        <button id="delete">삭제</button>
        <hr />
        <h2>내용</h2>
        <div id="save">
            <!--해당 영역에 데이터가 작성된다.-->
        </div>
        <script>
            window.addEventListener("load", function () {
                let data = localStorage.getItem("data");
                if (data != null) {
                    document.querySelector("#save").innerText =
                        JSON.parse(data);
                }
            });
        </script>

        <script>
            // 현재 하나의 데이터만 자꾸 가지고 처리한다.
            // 데이터가 여러개일 때는? 배열 사용

            // 등록 이벤트
            let createBtn = document.querySelector("#create");
            createBtn.addEventListener("click", function () {
                // let inputData = document.querySelector("#input").value;
                let inputTag = document.querySelector("#input");
                console.log(inputTag.value);
                console.log(typeof inputTag.value); // 해당 메서드를 통해 타입 확인 가능
                // 데이터를 저장하기 위해서 localStorage를 사용하자
                // 현재는 input 데이터가 string이라서 그냥 냅다 넣었다.

                // 객체를 문자열로 만들고 싶어
                let jsonData = JSON.stringify(inputTag.value);

                // 키와 벨류는 문자열로 넣어줘
                localStorage.setItem("data", jsonData);

                inputTag.value = "";
            });

            // 조회 이벤트 처리
            document
                .querySelector("#read")
                .addEventListener("click", function () {
                    let saveTag = document.querySelector("#save");

                    // 어떤 데이터를 가져와 넣을 것인가.
                    // 찾고자하는 key가 없으면 null이 반환된다.
                    let jsonData = localStorage.getItem("data");
                    // console.log(jsonData);
                    if (jsonData != null) {
                        let data = JSON.parse(jsonData);
                        saveTag.innerHTML = data;
                    }
                });

            // 삭제 이벤트
            document
                .querySelector("#delete")
                .addEventListener("click", function () {
                    localStorage.removeItem("data");
                    document.querySelector("#save").innerText = "";
                });
        </script>
    </body>
</html>
```

# AJAX
## 집안일 목록
- 우리는 동기적으로 일할 것이다.
- 치킨 주문하기
  - 치킨 먹기
- 세탁기에 빨래 넣고 돌리기
  - 빨래 건조기 넣고 돌리기
- 로봇 청소기 비우기
  - 로봇 청소기 비우기
- 걸레질 하기
- 쓰레기 버리고 하기

![stack](https://github.com/namoo1818/TIL/assets/50236187/4e1e3935-bb8b-4d23-a6b7-8c575a1a52dc)
- 먼저 차례대로 stack으로 일이 올라온다.
- 비동기적으로 일을 해야하는 것들이 들어오면 언제 처리될지 모르니까 Web API 영역으로 날려보낸다.
- 만약 집안일 목록을 처리하는 와중에 "치킨 주문하기"가 끝났다면 "치킨 먹기" 작업이 Task Queue로 올라한다.
- event loop가 task queue를 감시하고 있다가 stack이 한가할 때 작업을 차례대로 stack에 올린다.
- stack에 올라간 작업은 Web API로 이동돼서 처리된다.

## JavaScript는 Single thread
- 이벤트를 처리하는 Call Stack이 하나
- 즉시 처리하지 못하는 이벤트들을 (Web API)로 보내서 처리
- 처리된 이벤트들은 처리된 순서대로 (Task queue)에 저장
- Call Stack이 공백이 되면 (Event Loop)가 대기 줄에서 가장 오래된 이벤트를 Call Stack으로 보냄

# 동기와 비동기
<img href="동기와 비동기" src="https://github.com/namoo1818/TIL/assets/50236187/e32644e4-3eb3-4836-9377-a47fe690060e" width=500>
<br>

## 동기(Synchronous)
- 데이터의 요청과 결과가 한 자리에서 동시에 일어나는 것.
- 요청을 하면 시간이 얼마나 걸리던지 요청한 자리에서 결과가 주어진다.
```javascript
function doStep1(init) {
    return init + 1;
}

function doStep2(init) {
    return init + 2;
}

function doStep3(init) {
    return init + 3;
}

function doOperation() {
    let result = 0;
    result = doStep1(result);
    result = doStep2(result);
    result = doStep3(result);
    console.log(`result: ${result}`);
}

doOperation();
```
```
result: 6
```
## 비동기(Asynchronuos)
- 요청한 결과는 동시에 일어나지 않는다.
```javascript
function doStep1(init, callback) {
    const result = init + 1;
    callback(result);
}

function doStep2(init, callback) {
    const result = init + 2;
    callback(result);
}

function doStep3(init, callback) {
    const result = init + 3;
    callback(result);
}

// 콜백헬: 깊이 들어가면 지옥이 시작된다. -> promise로 해결
function doOperation() {
    doStep1(0, result1 => {
        doStep2(result1, result2 => {
            doStep3(result2, result3 => {
                console.log(`result: ${result3}`);
            });
        });
    });
}

doOperation();
```
```
result: 6
```


# AJAX(Asynchronous JavaScript and XML)
- 비 동기식 JavaScript와 XML
- 서버와 통신을 하기 위해서 XMLHttpRquest 객체 활용
- JSON, XML, HTML 그리고 일반 텍스트 형식 들을 포함한 다양한 포맷을 주고 받을 수 있음. 예를 들어 지도.
- 페이지 전체를 '새로고침'하지 않고서도 수행되는 '비동기성'(일 부분만 업데이트 가능)
- 왜 비동기성을 사용하나? 사용자 경험(편하니까)

# 동작 방식
- 위에는 옛날 방식(동기식), 아래는 요즘 방식(비동기식)
![동작방식](https://github.com/namoo1818/TIL/assets/50236187/82af7a29-b284-47e6-9be4-85e52d5207d3)

# 순차적인 비동기 처리하기(내일 할 내용)
- Web API로 들어오는 순서는 중요하지 않고, 어떤 이벤트가 먼저 처리되느냐가 중요(실행 순서 불명확)
- 동기처럼 처리할 수 있게 만드는 방법 2가지
1. Async Callbacks
   - 백그라운드에서 실행을 시작할 함수를 호출할 때 인자로 지정
   - ex) addEventListener()의 두번째 인자
2. Promise-Style
   - Modern Web APIs에서의 새로운 코드 스타일
   - XMLHttpRequest 객체를 사용하는 구조보다 조금 더 현대적인 버전

# XMLHttpRquest 객체
- JavaScript Object
- 서버와 상호작용하기 위해 사용
- 전체 페이지의 새로고침 없이도 URL로부터 데이터를 받아올 수 있음(주식 화면을 생각해보자)
- 사용자의 작업을 방해하지 않고 페이지의 일부를 업데이트할 수 있다
- AJAX 프로그래밍에 주로 사용
- XML이라는 이름과는 달리 모든 종류의 데이터를 받아오는데 사용 가능
- http 이외의 프로토콜도 지원(file, ftp 포함)
- 대부분의 브라우저에서 지원

# XMLHttpRequest 객체의 메서드를
- open("Http method", "URL", sync/async)
  - 요청의 초기화 작업
  - GET/POST 지정
  - 서버 URL 지정
  - 동기/비동기 설정
- send(content)
  - GET 방식은 URL에 필요한 정보를 추가하기 때문에 null 적용
  - POST 방식에서 파라미터 설정 처리

# XMLHttpRequest 객체 프로퍼티들
- onreadystatechange
  - 서버에서 응답이 도착했을 때 호출될 콜백함수 지정
  - 콜백함수는 상태(readyState)가 변경될 때마다 호출
- readyState (숫자도 괜춘, 영어도 괜춘)
  - 0 -> UNSENT(객체 생성 후 open 메서드 호출 전)
  - 1 -> OPEND(open 메서드가 호출되고 send 호출 전)
  - 2 -> HEADERS_RECEIVED(send 메서드가 호출되었지만 서버 응답 전, 헤더와 상태 확인 가능)
  - 3 -> LOADING(다운로드 중, 데이터의 일부가 전송된 상태)
  - 4 -> DONE(모든 데이터 전송 완료)

# XMLHttpRequest 프로퍼티들
- staus
  - 서버 처리 결과 상태 코드
  - 200 -> OK(요청 성공)
  - 404 -> Not Found(페이지를 못 찾을 경우)
  - 500 -> Server Error(서버에서 결과 생성 시 오류 발생)
- responseText
  - 서버의 응답결과를 문자열로 받기
- responseXML
  - 서버의 응답결과를 XML Document로 받기

# AJAX 프로그래밍 순서
1. 클라이언트 이벤트 발생
2. XMLHttpRequest 객체 생성
3. XMLHttpRequest 객체 콜백함수 설정
4. XMLHttpRequest 객체를 통한 비동기화 요청
5. 서버 응답결과를 생성하여 클라이언트로 전송
6. XMLHttpRequest 객체는 서버 결과를 처리할 콜백함수 호출
7. 결과를 클라이언트 화면에 반영

# 실습
```javascript
console.log("Hi");
setTimeout(function () {
    console.log("대기끝");
}, 3000);
console.log("Bye");
```
```
Hi
Bye
(3초 후에) 대기끝
```
-  "대기끝"이 출력되는데 3초보다 더 걸릴 수 있음
```javascript
console.log("Hi");
setTimeout(function () {
    console.log("대기끝");
}, 0);
console.log("Bye");
```
```
Hi
Bye
대기끝
```
- 대기시간이 0초라고 해도 setTimeout 자체가 비동기 함수라서 일단 Web api로 보내버린다.

```javascript
setInterval(function () {
    let bgColor = document.body.style.background;
    if (bgColor == "red") document.body.style.background = "yellow";
    else document.body.style.background = "red";
}, 1000);
```
- 1초마다 배경화면이 빨간색, 노란색으로 바뀐다.


```javascript
// 아래의 URL로 요청을 보내면 JSON 형태의 데이터를 돌려준다.
const URL = "https://jsonplaceholder.typicode.com/todos/1";

// AJXA 통신할거야
const xhr = new XMLHttpRequest();

// xhr를 통신 서버에 요청을 보내기 위해서...
xhr.open("GET", URL); // 초기화 작업
xhr.send();

// JS 싱글스레드라서 기다리지 않는다.
// 응답이 오지 않는 상태에서 처리하려고 해서 todo에는 값이 없고 브라우저에서 써보면 나온다.
const todo = xhr.response;
console.log(todo); // 안떠
```

```javascript
// 아래의 URL로 요청을 보내면 JSON 형태의 데이터를 돌려준다.
const URL = "https://jsonplaceholder.typicode.com/todos/1";

// AJXA 통신할거야
const xhr = new XMLHttpRequest();

// xhr를 통신 서버에 요청을 보내기 위해서...
xhr.open("GET", URL); // 초기화 작업
xhr.send();

// 해당 속성은 상태가 바뀔 때마다 수행할 콜백메서드를 지정한다.
xhr.onreadystatechange = function () {
    if (xhr.readyState == 4) {
        // if(xhr.readyState == xhr.DONE){
        if (xhr.status == 200) {
            const todo = xhr.response;
            console.log(todo);
        }
    }
};
```

```
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

- data 받아서 화면에 출력하기
- LiveServer로 켜야 데이터를 가져올 수 있다.
```javascript
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8" />
        <title>XMLHttpRequest실습</title>
    </head>
    <body>
        <h2>서버에 요청을 보내고 받아서 화면에 출력하자</h2>
        <div id="view"></div>
        <button id="submit">요청</button>

        <script>
            let xhr;
            //클라이언트에서 요청이 발생한다.
            document
                .querySelector("#submit")
                .addEventListener("click", function () {
                    //xhr 객체를 생성한다.
                    xhr = new XMLHttpRequest();
                    xhr.onreadystatechange = responseMsg;
                    //xhr 객체 초기화 (URL 입력, 메소드 방식 설정....)
                    //마지막 true의 의미는 비동기방식의 여부
                    xhr.open("GET", "./data/hello.txt", true);
                    //요청 보내기
                    xhr.send();
                });

            //AJXA 요청에 대한 응답이 왔을때 사용할 콜백함수
            function responseMsg() {
                //서버의 응답이 끝났을 때
                if (xhr.readyState == 4) {
                    //서버에서 오류없이 정상적으로 처리가 되었을때
                    if (xhr.status == 200) {
                        document.querySelector("#view").innerHTML =
                            xhr.responseText;
                    } else {
                        console.log("정상적으로 데이터를 받지 못했다.");
                    }
                }
            }
        </script>
    </body>
</html>
```

```
<table style="width: 50%; border: 3px solid tomato">
  <tr>
    <td>ajax</td>
    <td>is</td>
    <td>easy</td>
  </tr>
</table>
```
![캡처](https://github.com/namoo1818/TIL/assets/50236187/a4cd4a4d-130e-40af-8e37-58b1aae52a0c)

```javascript
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8" />
        <title>XMLHttpRequest실습</title>
    </head>
    <body>
        <!-- https://dog.ceo/api/breeds/image/random 한번해보기 ㅎ -->
        <h2>서버에 요청을 보내고 JSON 데이터를 받아 화면에 출력하자</h2>
        <div id="view"></div>
        <button id="submit">요청</button>

        <script>
            let xhr;
            //클라이언트에서 요청이 발생한다.
            document
                .querySelector("#submit")
                .addEventListener("click", function () {
                    //xhr 객체를 생성한다.
                    xhr = new XMLHttpRequest();
                    xhr.onreadystatechange = responseMsg;
                    //xhr 객체 초기화 (URL 입력, 메소드 방식 설정....)
                    //마지막 true의 의미는 비동기방식의 여부
                    xhr.open("GET", "./data/member.json", true);
                    //요청 보내기
                    xhr.send();
                });

            //AJXA 요청에 대한 응답이 왔을때 사용할 콜백함수
            function responseMsg() {
                //서버의 응답이 끝났을 때
                if (xhr.readyState == 4) {
                    //서버에서 오류없이 정상적으로 처리가 되었을때
                    if (xhr.status == 200) {
                        let studentList = JSON.parse(xhr.response);
                        console.log(studentList);
                        //배열이 넘어왔으니 요소를 반복문을 돌면서 화면에 추가하면 되겠다.
                    } else {
                        console.log("정상적으로 데이터를 받지 못했다.");
                    }
                }
            }
        </script>
    </body>
</html>

```
```
[
  {
    "id": "ko",
    "name": "고싸피"
  },
  {
    "id": "jang",
    "name": "장싸피"
  },
  {
    "id": "park",
    "name": "박싸피"
  }
]

```
![캡처2](https://github.com/namoo1818/TIL/assets/50236187/fa819153-ef65-4d40-9aea-3e0c29977c9a)

# 기타
- 강아지 사진을 돌려주는 API
- 한번 해보세용
- https://dog.ceo/dog-api
