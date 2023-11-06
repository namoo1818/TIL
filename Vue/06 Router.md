### 2023.11.06
# Routing
> 네트워크에서 경로를 선택하는 프로세스    
> 웹 어플리케이션에서 다른 페이지 간의 전환과 경로를 관리하는 기술

# SSR(Server Side Rendering)에서의 Routing
- 서버가 사용자가 방문한 URL 경로를 기반으로 응답을 전송
- 링크를 클릭하면 브라우저는 서버로부터 HTML 응답을 수신하고 HTML로 전체 페이지를 다시 로드

# CSR(Single Page Application) / SPA(Client Side Rendering)에서의 Rounting
- SPA에서 routing은 브라우저의 **클라이언트 측**에서 수행
- 클라이언트 측 JavaScript가 새 데이터를 동적으로 가져와 전체 페이지를 다시 로드하지 않음
- 페이지는 1개이지만, 링크에 따라 여러 컴포넌트를 렌더링하여 마치 여러 페이지를 사용하는 것처럼 보이도록 해야 함

# Vue Router
- https://v3.router.vuejs.org/kr/installation.html  (시간날 때 정독)   
- Vue2는 Router3, Vue3는 Router4 사용
- 우리 수업은 컴포지션 API 사용

- vue project 생성 시 Add Vue Router 허용한다  
- 라우터 url에 about이 생김 http://localhost:5173/about
- 화면을 두개로 나눠 사용
- RouterLink : 실제로는 a 태그
- RouterView : url에 해당하는 컴포넌트를 표시

- createWebHashHistory 는 url에 #이 들어감 좀 구림 localhost:5173/#/board
- createWebHistory 사용을 권장
- routes 배열 : URI 경로와 컴포넌트(views)를 매핑
- index.js가 내보낸 router를 main.js가 받는다
- views
- components에는 about, Homeview가 있다

- 라우팅 기본
- 이름 안써도 ok. 주소와 컴포넌트만 적어도 괜찮아


# Named Routes 
- name 속성 값에 경로에 대한 이름을 지정
- 오타 방지 good
```js
// index.js
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      component: AboutView
    }
  ]
})
```
```vue
<!-- App.vue -->
<RouterLink :to="{name: 'home'}">HomeName</RouterLink>
<RouterLink :to="{name: 'about'}">AboutName</RouterLink>
```
# 네비게이션 가드
> Vue router를 통해 특정 URL에 접근할 때 다른 URL로 redirect를 하거나 취소하여 네비게이션을 보호
- Globally (전역 가드)
  - router.before
- 라우터 가드
- 컴포넌트 가드

- router.push()
- router.replace() : 현재 위치 바꾸기

# 실습
- 양띵균userview라서 기존의 컴포넌트에서 활용하기 때문에 값이 바뀌지 않는다

# 컴포넌트 가드
- onBeforeRouteLeave
- onBeforeRouteUpdate
- onBeforeRouteLeave
  - 현재 라우트에서 다른 라우트로 이동하기 전에 실행
  - 사용자가 현재 페이지를 떠나는 동작에 대한 로직을 처리
- onBeforeRouteUpdate
  - 이미 렌더링된 컴포넌트가 같은 라우트 내에서 업데이트 되기 전에 실행
  - 라우트 업데이트 시 추가적인 로직을 처리
