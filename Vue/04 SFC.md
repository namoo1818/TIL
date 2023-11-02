### 2023.11.02
# Component 특징
> 재사용 가능한 코드 블록
- UI를 독립적으로 재사용 가능한 일부분으로 분할하고 각 부분을 개별적으로 다룰 수 있음
- 자연스럽게 앱은 중첩된 Component 트리로 구성됨       
![component](https://github.com/namoo1818/TIL/assets/50236187/ad59ad87-0238-4987-b638-6481c617a0f7)

# SFC(Single-File Components)
> 컴포넌트의 템플릿, 로직 및 스타일을 하나의 파일로 묶어낸 특수한 파일 형식(*.vue 파일)
- Vue SFC는 HTML, CSS, JS 를 하나로 합친 것
- <template>, <script> 및 <style> 블록은 하나의 파일에서 컴포넌트의 뷰, 로직 및 스타일을 캡슐화하고 배치
- <template> : 실제 화면에 렌더링 되진 않지만 JS로 동적 조작이 가능
- 최상위 template 태그는 1개만! 
- Syntax 문법
- 실제 프로젝트에서 SFC 컴파일러는 Vite와 같은 공식 빌드 도구를 사용

![Vue SFC Playground](https://github.com/namoo1818/TIL/assets/50236187/3cbf76c9-3c62-40f4-b951-29e790e4c53d)

# 사전 준비
- Node.js 다운로드
- VS code에서 Vue Language Features (Volar) 다운로드
- 편리한 자동 완성 확장 앱 : Vue 3 Snippets, Vue VSCode Snippets

# Node.js
- 일반적인 JS는 브라우저에서만 실행했는데 외부에서도 실행되게 한 기술
- Chrome의 V8 JavaScript 엔진을 기반으로 하는 Server-Side 실행환경
- NPM(Node Package Manager) : Node.js의 기본 패키지 관리자

# Vite 프로젝트 구조(node-modules)
- Node.js 프로젝트에서 사용되는 외부 패키지들이 저장되는 디렉토리
- 프로젝트의 의존성 모듈을 저장하고 관리하는 공간
- 프로젝트가 실행될 때 필요한 라이브러리와 패키지들을 포함
- 파일이 많고 크기 때문에 .gitIgnore에 작성됨

## package-lock.json
- 패키지 설치에 필요한 모든 정보 포함
- 패키지들의 정확한 버전 보장 -> 협업 시 충돌 방지
- npm install 명령 시 명시된 버전과 의존성을 기반으로 설치(우리가 버전 신경쓸 필요 x)

## package.json
- 프로젝트 메타 정보와 의존성 패키지 목록 포함
- 프로젝트 이름, 버전, 작성자. 라이선스 등과 같은 메타 정보 정의
- package-lock.json 과 함께 프로젝트의 의존성을 관리하고, 버전 충돌 및 일관성을 유지하는 역할

## favicon
- 탭에 뜨는 아이콘 이미지

## src/App.vue
- Vue 앱의 최상위 Root 컴포넌트

## index.html
- Root 컴포넌트인 App.vue가 해당 페이지에 마운트(mount)됨

# Module
> 프로그램을 구성하는 독립적인 코드 블록(*.js 파일)
- 모듈이 많아지고 라이브러리 또는 모듈 간의 의존성이 깊어지면서 특정한 곳에서 문제가 발생하면 찾기 어려워짐
- 모듈의 의존성 문제 해결 도구 -> Bundler

# 실습
- App.vue
```
<script setup>
// 상대경로
// import MyComponent from "./components/MyComponent.vue";
// @:절대경로
import MyComponent from "@/components/MyComponent.vue";
</script>
```
# Component 이름 - Vue 스타일 가이드
https://ko.vuejs.org/style-guide/rules-strongly-recommended.html

## 케밥 케이스 가능
```
<template>
    <div>
        <h2>App.vue</h2>
        <!--둘 다 가능-->
        <!--<MyComponent/>-->
        <my-component></my-component>
    </div>
</template>
<script setup>
import MyComponent from "@/components/MyComponent.vue";
</script>

<style></style>
```

# Virtual DOM
- 가상의 DOM을 메모리에 저장하고 실제 DOM과 동기화하는 프로그래밍 개념
- 실제 DOM과의 변경 사항 비교를 통해 변경된 부분만 실제 DOM에 적용하는 방식
- 웹 어플리케이션의 성능을 향상시키기 위한 Vue의 내부 렌더링 기술
## 장점
- 효율성 : 실제 DOM 조작을 최소화, 변경된 부분만 업데이트하여 성능 향상
- 반응성 : 데이터 변경 감지(watch, computed), Virtual DOM을 효율적으로 갱신하여 UI를 자동으로 업데이트
  - watch : 감시하고 있는 특정 데이터가 바뀔 때마다 갱신
  - computed : 캐싱하고 있다 의존성 있는 데이터가 바뀔 때마다 갱신
- 추상화 : 개발자는 실제 DOM 조작을 Vue에 맡기고 컴포넌트와 템플릿을 활용하는 추상화된 프로그래밍 방식으로 원하는 UI 구조를 구성하고 관리할 수 있음
## 주의사항
- 실제 DOM에 직접 접근하지 말 것(JS에서 사용하는 DOM 접근 관련 메서드 사용 금지!)
- Vue의 ref와 Lifecycle Hooks 함수를 사용해 간접적으로 접근하여 조작할 것

# API 스타일 2가지
## Composition API
- import해서 가져온 API 함수들을 사용하여 컴포넌트의 로직을 정의
- Vue3에서의 권장 방식
- 규모가 있는 앱의 전체를 구축할 때 SFC와 함께 사용
## Option API
- data, methods 및 mounted 같은 객체를 사용하여 컴포넌트의 로직을 정의
- Vue2에서의 작성 방식
- 빌드 도구를 사용하지 않거나 복잡성이 낮은 프로젝트에서 사용    
<img href="api" src="https://github.com/namoo1818/TIL/assets/50236187/faea11c9-abeb-4682-8051-a3e64ddf8350" width=500>

# Scaffolding(스캐폴딩)
- 새로운 프로젝트나 모듈을 시작하기 위해 초기 구조와 기본 코드를 자동으로 생성하는 과정

# 추가
### SFC의 CSS 기능 - scoped
### 모든 컴포넌트에는 최상단 HTML 요소를 작성하는 것을 권장
### 관심사항의 분리가 파일 유형의 분리와 동일한 것은 아니다
- ppt 참고
