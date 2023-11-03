### 2023.11.03
- 한 페이지를 구성하는 컴포넌트가 여러 개라면 각 컴포넌트가 개별적으로 같은 데이터를 관리해야 할까?
- 사진을 변경하면 모든 컴포넌트에게 변경 요청을 해야한다. 매우 불편
- **공통된 부모 컴포넌트에서 관리하자**

# Passing Props
> 부모는 자식에게 데이터를 전달(Pass Props)     
  자식은 자신에게 일어난 일을 부모에게 알림(Emit event)
- 단방향     
- 은행(부모), 고객(자식)   
  고객은 은행에게 돈(데이터)를 보내거나 받고,
  은행은 고객에게 통장 잔액(알림)을 알려준다.

# Props 특징
- 부모 속성이 업데이트되면 자식으로 흐르지만 그 반대는 안됨
- 자식 컴포넌트 내부에서 props를 변경하려고 시도해서는 안되며 불가능하다
- 부모 컴포넌트가 업데이트 될 때마다 자식 컴포넌트의 모든 props가 최신 값으로 업데이트된다

# Props 선언
- 부모 컴포넌트에서 보낸 props를 사용하기 위해서는 자식 컴포넌트에서 명시적인 props 선언이 필요하다
## 방법 1. 문자열 배열을 사용한 선언
```
defineProps(["myMsg"]);
```
## 방법 2. 객체를 사용한 선언
```
const props = defineProps({
    myMsg: String,
});
```

# Passing Props
## 1. Props Name Casing
- 선언 및 템플릿 참조 시 -> camelCase
- 자식 컴포넌트로 전달 시 -> kebab-case
```
<template>
    <div>
        <h3>자식 컴포넌트</h3>
        <p>{{ myMsg }}</p>
        <p>{{ dynamicProps }}</p>
        <ParentGrandChild :my-msg="myMsg" />
    </div>
</template>
```
## 2. Static props & Dynamic props



# Component Events
## $emit()
> 자식 컴포넌트가 이벤트를 발생시켜 부모 컴포넌트로 데이터를 전달하는 역할의 메서드
## 이벤트 발신 및 수신하기

# 이벤트 인자(Event Arguments)
> 이벤트 발신 시 추가 인자를 전달하여 값을 제공할 수 있다

# Event Name Casing
- 선언 및 발신 시 -> camelCase
- 부모 컴포넌트에서 수신 시 -> kebab-case

# Prop 선언을 객체 선언 문법으로 권장하는 이유
- 가독성이 좋고 prop에 대한 유효성 검사로써 활용이 가능하다
