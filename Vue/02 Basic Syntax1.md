### 2023.10.31

# Attribute Bindings
```javascript
<div id="my-id"></div>
```
- body에 작성
```javascript
<div v-bind:id="dynamicId"></div>
```
- 변수 선언(script에 작성)
```javascript
const dynamicId = ref('my-id')
```
- 콧수염 구문은 HTML 속성 내에서 사용할 수 없기 때문에 v-bind를 사용
- HTML의 id 속성 값을 vue의 dynamicId 속성과 동기화 되도록 함
- 바인딩 값이 null이나 undefind인 경우 렌더링 요소가 제거됨

# JavaScript Expressions
```javascript
{{number+1}}
{{ok? 'YES':'NO'}}
{{message.split('').reverse().join('')}}
<div:id="`list-${id}`"></div>
```
- `:`은 v-bind의 약어
- Vue는 모든 데이터 바인딩 내에서 JavaScript 표현식의 모든 기능을 지원
- Vue 템플릿에서 JavaScript 표현식을 사용할 수 있는 위치
  - 콧수염 구문 내부
  - 모든 directive의 속성 값(v-로 시작하는 특수 속성)

# v-on 구성
- DOM 요소에 이벤트 리스너를 연결 및 수신

# 단방향 데이터 바인딩
- 데이터 흐름이 단방향적입니다. 즉, 모델(데이터) => 뷰(화면)로만 데이터가 이동
- 사용자가 UI에서 데이터를 변경하더라도 모델의 데이터는 직접적으로 변경 X

# 양방향 데이터 바인딩
- 데이터가 양쪽으로 흐른다. 즉, 모델의 변경이 뷰에 자동으로 반영되고, 뷰의 변경이 모델에 자동으로 반영
- 사용자가 UI의 특정 부분을 변경하면 모델도 변경된다. 그리고 모델의 변경은 뷰에도 자동으로 반영
- v-model은 양방향 바인딩
