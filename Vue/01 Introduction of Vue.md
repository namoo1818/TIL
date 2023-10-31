### 2023.10.30
- Back-End에서는 REST API 형태로 만들었다
-  AJAX : 클라이언트와 서버 간에 데이터를 주고 받기 위해 HTTP 통신을 사용한다. js에서 비동기 HTTP 통신을 위해 사용하는 개발 기법.
  - xhr, fetch, axios 등이 있다

# Front-End
- 웹 사이트와 웹 어플리케이션의 사용자 인터페이스(UI)와 사용자 경험(UX)을 만들고 디자인하는 것
- HTML, CSS, JavaScript 등을 활용하여 사용자가 직접 상호작용하는 부분을 개발
- Front-End framework 3대장 : React, Angular, Vue.js

# Client-side Frameworks가 필요한 이유
- 웹에서 하는 일이 많아졌다 -> `웹 어플리케이션`의 등장
- 다루는 데이터가 많아졌다 -> 어플리케이션의 상태를 변경할 때마다 일치하도록 UI를 업데이트해야 한다

# Single Page Application(SPA)
> 페이지 한 개로 구성된 웹 어플리케이션
- 서버로부터 필요한 모든 정적 HTML을 처음에 한번 가져온다
- 브라우저가 페이지를 로드하면 Vue 프레임워크는 각 HTML 요소에 적절한 JavaScript 코드를 실행한다

# Client-side Rendering(CSR)
> 클라이언트에서 화면을 렌더링하는 방식
- 브라우저는 페이지에 필요한 최소한의  HTML 페이지와 JavaScript를 다운로드
- JavaScript를 사용하여 DOM을 업데이트하고 페이지를 렌더링

# CSR의 장단점
## 장점
1. 빠른 속도
  - 페이지 일부를 다시 렌더링할 수 있으므로 동일한 웹 사이트의 다른 페이지로 이동이 빠르다
  - 서버로 전송되는 데이터의 양 최소화
2. 사용자 경험
  - 새로 고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험을 제공
3. Front-End와 Back-End의 명확한 분리
  - Front-End : UI 렌더링 및 사용자 상호 작용 처리
  - Back-End : 데이터 및 API 제공
  - 대규모 어플리케이션을 더 쉽게 개발하고 유지 관리 가능
## 단점
1. 초기 구동속도가 느림
   - 전체 페이지를 보기 전에 약간의 지연을 느낄 수 있다
2. SEO(검색 엔진 최적화) 문제
   - 페이지를 나중에 그려 나가는 것이기 때문에 검색에 잘 노출되지 않을 수 있다

# Vue.js
> 사용자 인터페이스를 구축하기 위한 JavaScript 프레임워크

![vue](https://github.com/namoo1818/TIL/assets/50236187/db5cd1ba-2baf-4484-a03b-557d66187980)

# Vue 장점
1. 쉬운 학습 곡선 및 간편한 문법
   - 새로운 개발자들도 빠르게 학습할 수 있음
2. 반응성 시스템
   - 데이터 변경에 따라 자동으로 화면이 업데이트 되는 기능 제공
3. 모듈화 및 유연한 구조
   - 어플리케이션을 컴포넌트 조각으로 나눌 수 있다
   - 코드의 재사용성을 높이고 유지보수를 용이하게 한다

# Vue의 2가지 핵심 기능
1. 선언적 렌더링(Declarative Rendering)
   - HTML을 확장하는 템플릿 구문을 사용하여 HTML이 JavaScript 데이터를 기반으로 어떻게 보이는지 설명할 수 있음
2. 반응형(Reactivity)
   - JavaScript 상태 변경사항을 자동으로 추적하고 변경사항이 발생할 때 DOM을 효율적으로 업데이트

# Vue 시작하기
- 크롬에서 Vue.js devtools 확장 프로그램 설치

1. `CDN 방식(Content Delivery Network)`(우리는 이거 선택)
2. NPM 방식(Node Package Manager)

### CDN 방식
- html에 스크립트 추가
```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```
### 첫번째 Vue 작성하기
- 모든 Vue 어플리케이션은 `createApp` 함수로 새 Application instance를 생성하는 것으로 시작
```html
<body>
    <script>
        const { createApp } = Vue; // 구조 분해 할당
        // 2. Application Instance 생성

        const app = createApp();
    </script>
</body>
```
- `app.mount()`
  - 컨테이너 요소에 어플리케이션 인스턴스를 탑재(연결)
  - 각 앱 인스턴스에 대해 mount()는 한 번만 호출할 수 있다
```html
<body>
    <div id="app"></div>
    <script>
        const { createApp } = Vue; // 구조 분해 할당
        // 2. Application Instance 생성

        const app = createApp();

        // 3. dom에 연결하겠다.
        app.mount("#app");
    </script>
</body>
```
- `ref 함수` : 반응형 상태(데이터)를 선언하는 함수. 반응형을 가지는 참조 변수를 만드는 것.
- 인자를 받아 .value 속성이 있는 ref 객체로 래핑하여 반환
- ref로 선언된 변수의 값이 변경되면, 해당 값을 사용하는 템플릿에서 자동으로 업데이트
- 인자는 모든 타입 가능
```html
<div id="app">
<p>{{message}}</p>
</div>
<script>
const { createApp, ref } = Vue; // 구조 분해 할당
// 2. Application Instance 생성

const app = createApp({
    setup() {
        const message = ref("Hello Vue!");
        console.log(message);
        console.log(message.value);
    },
});

// 3. dom에 연결하겠다.
app.mount("#app");
</script>
```
![ref](https://github.com/namoo1818/TIL/assets/50236187/3560de04-e1dc-42f6-9602-6b76874fbcd8)
- 템플릿 참조에 접근하려면 setup 함수에서 선언 및 반환 필요
- 템플릿에서 ref를 사용할 때는 .value를 작성할 필요 없음(automatically unwrapped)
- 화면에 `Hello Vue!` 출력
```
<div id="app">
<p>{{message}}</p>
</div>
<script>
    const { createApp, ref } = Vue; // 구조 분해 할당
    // 2. Application Instance 생성

    const app = createApp({
        setup() {
            const message = ref("Hello Vue!");

            return {
                message,
            };
        },
    });

    // 3. dom에 연결하겠다.
    app.mount("#app");
</script>
```

# Vue 기본 구조
- createApp()에 전달되는 객체는 Vue 컴포넌트(Component)
- 컴포넌트의 상태는 setup() 함수 내에서 선언되어야 하며 **객체를 반환해야 함**

# 템플릿 렌더링
- 반환된 객체의 속성은 템플릿에서 사용할 수 있다
- Mustache syntax(콧수염 구문)를 사용하여 메시지 값을 기반으로 동적 텍스트를 렌더링
- 콘텐츠는 식별자나 경로에만 국한되지 않으며 유효한 JavaScript 표현식을 사용할 수 있다
```html
<div id="app">
    <p>{{message}}</p>
    <p>{{message.split('').reverse().join('')}}</p>
</div>
```
```
Hello Vue!
!euV olleH
```

# Event Listeners in Vue
- 'v-on' directive를 사용하여 DOM 이벤트를 수신할 수 있다
- 함수 내에서 refs를 변경하여 구성 요소 상태를 업데이트
- 단방향
- v-on의 약어:@
- 누르면 1씩 증가하는 버튼을 만들자
```html
<div id="app">
    <button @:click="increment">{{count}}</button>
</div>
<script>
    const { createApp, ref } = Vue;

    const app = createApp({
        setup() {
            const count = ref(0);
            // 함수 표현식
            const increment = function () {
                count.value++;
            };
            return {
                count,
                increment,
            };
        },
    });

    app.mount("#app");
</script>
```
![v-on](https://github.com/namoo1818/TIL/assets/50236187/31052c46-ea48-45be-97aa-2043b1dabd70)

# 참고
![unwrap주의사항](https://github.com/namoo1818/TIL/assets/50236187/0a8bc549-9b75-4da2-82b4-95393cbd7eb3)
![unwrap주의사항2](https://github.com/namoo1818/TIL/assets/50236187/53dc47ad-cc13-4945-88b2-5d084356cc9a)
![unwrap주의사항3](https://github.com/namoo1818/TIL/assets/50236187/10e28758-f8cf-4ec7-b601-7255b5c5b105)


```html
<div id="app">
  <div>{{object.id +1}}</div>
  <div>{{object["id"]+1}}</div>
  <div>{{object.id}}</div>
  <div>{{object.id.value}}</div>
  <div>{{object.id.value + 1}}</div>
  <div>{{object["id"]}}</div>
  <div>{{id}}</div>
  <div>{{id+1}}</div>
</div>
<script>
  const { createApp, ref } = Vue;

  const app = createApp({
    setup() {
      const object = {
        id: ref(0),
      };

      const { id } = object; //구조분해할당

      return {
        object,
        id,
      };
    },
  });
  app.mount("#app");
</script>
```
```
[object Object]1
[object Object]1
0
0
1
0
0
1
```

# 반응형 변수와 일반 변수
- 반응형 변수만 1씩 증가한다
```html
<div id="app">
  <div>반응성 변수 : {{reactiveValue}}</div>
  <div>일반 변수 : {{normalValue}}</div>
  <button @click="updateValues">값 업데이트</button>
</div>
<script>
  const { createApp, ref } = Vue;

  const app = createApp({
    setup() {
      const reactiveValue = ref(100); //반응형 변수
      const normalValue = 10; //그냥 변수
      const updateValues = function () {
        reactiveValue.value++;
        normalValue++;
      };
      return {
        reactiveValue,
        normalValue,
        updateValues,
      };
    },
  });
  app.mount("#app");
</script>
```
![반응형 변수](https://github.com/namoo1818/TIL/assets/50236187/54f32f7d-0916-4b29-9bf3-b58a55029a3e)

# SEO
- Search Engine Optimization
- goole, bing과 같은 검색 엔진 등에 내 서비스나 제품 등이 효율적으로 검색 엔진에 노출되도록 개선하는 과정을 일컫는 작업

# CSR
- Client Side Rendering
- 렌더링이 클라이언트 쪽에서 일어난다
- 서버는 요청을 받으면 클라이언트에 HTML과 JS를 보내주고 클라이언트는 그것을 받아 렌더링을 한다.

# SSR
- Server Side Rendering
- 서버쪽에서 렌더링 준비를 끝마친 상태로 클라이언트에 전달하는 방식
- 서버에서 이미 '렌더 가능한' 상태로 클라이언트에 전달되기 때문에, JS가 다운로드 되는 동안 사용자는 무언가를 보고 있을 수 있다.

- 첫 페이지 로딩 시간은 평균적으로 SSR이 빠르고 나머지 로딩 시간은 CSR이 더 빠르다.
- 서버 자원은 SSR이 더 많이 사용한다.
