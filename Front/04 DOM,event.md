### 2023.08.03
# ⭐window 제공 함수
- alert, confirm, prompt, open, parseInt, parseFloat, seTimeout, clearTimeout, setInterval, clearInterval
![ex_screenshot](/images/window_제공_함수.png)
- DOM: 문서를 조작하기 위한 Object
- DOM: 브라우저를 조작하기 위한 Object
- JavaScript 자체 Object
```
window = {
  document : {
  }
}
```
# DOM(Document Object Model)
![ex_screenshot](/images/DOM.png)
- 문서를 객체지향적인 방법으로 모델화(도형화)
- XML, HTML 문서의 각 항목을 계층으로 표현하여 생성, 변형, 삭제할 수 있도록 돕는 인터페이스
- DOM은 문서 요소 집합을 트리 형태의 계층 구조로 HTML 표현
- HTML 문서의 요소를 제어하기 위해 지원
- 상단의 document 노드를 통해 접근

# 문서 접근 방식 이해
- getElementById(string)
- querySelector(css selector)
- querySelectorAll(css selector)
## querySelectorAll(css selector)
querySelector와 사용방식 동일  
결과를 배열처럼 사용  
```javascript
var list = document.querySelectorAll("div");
for(var i=0;i<list.length;i++) {
  console.log(list[i])
}
```

# 문서 조작 방식 이해
- createElement(tagName)
- createTextNode(text)
- appendChild(node)
- append(string | node)
- removeChild(node)
- setAttribute(name, value)
- innerHTML
- innerTEXT

## setAttribue(name, value)
```javascript
// attribute 수정
var ele = document.createElemens("img");
ele.setAttribute("src","./images/cake.jpg");
ele.setAttribute("width",200);
ele.setAttribute("height",150);
ele.setAttribute("msg", "test");
```
```javascript
<img src = "./images/cake.jpg"
    width = "200"
    height = "150"
    msg = "test"
>
```
_________________________________________
```javascript
// properity 수정
ele.src = "./images/cake.jpg";
ele.width = 200;
ele.height = 150;
ele.msg = "test";
```
```javascript
<img src = "./images/cake.jpg"
    width = "200"
    height = "150"
>
```
# Event
- (특히 중요한) 사건[일]
- 웹 페이지에서 여러 종류의 상호작용이 있을 때마다 이벤트가 발생
- 마우스를 이용했을 때, 키보드를 눌렀을 때 등 많은 이벤트가 존재
- JavaScript를 사용하여 DOM에서 발생하는 이벤트를 감지하고 대응하는 작업을 수행할 수 있음
![ex_screenshot](/images/event.JPG)

# 이벤트 종류
- 키보드 -> keyup, keydown, keypress
- 마우스 -> click, mousemove, mouseup, mousedown, mouseenter, mouseleave
- 로드 -> load, unload
- 폼 -> input, change, blur, focus, submit

# 이벤트 처리 방식의 이해
- 고전 이벤트 처리 방식 : attribute / property 방식으로 등록
- 표준 이벤트 처리 방식 : addEventListener 메서드 이용

# 고전 이벤트 처리 방식
- 인라인 이벤트 설정 -> 엘리먼트에 직접 지정
- 설정하려는 이벤트를 정하고 **on이벤트종류**의 형식으로 지정
![ex_screenshot](/images/고전이벤트처리방식.PNG)
- 엘리먼트에서 이벤트를 직접 설정하지 않고 스크립트에서 이벤트 설정
![ex_screenshot](/images/고전이벤트처리방식2.PNG)

# 표준 이벤트 처리 방식
- 이벤트 요소.addEventListener(이벤트타입, 이벤트리스너, [option]);
![ex_screenshot](/images/표준이벤트처리방식.PNG)

# 🌟이벤트 전파(Event propagation)
- 캡쳐링 단계(capturing phase) : 이벤트가 상위 요소에서 하위 요소 방향으로 전파 (html -> body -> div -> btn)
- 타깃 단계(target phase) : 이벤트가 타깃에 도달 (btn에 도달)
- 버블링 단계(bubling phase) : 이벤트가 하위 요소에서 상위 요소 방향으로 전파 (html <- body <- div <- btn)

# 고전 처리 방식 vs 표준 처리 방식
- 고전 처리 방식 : 타깃 단계와 버블링 단계의 이벤트만 캐치 가능
- 표준 처리 방식 : 타깃 단계와 버블릿 단계 뿐만 아니라 캡쳐링 단계의 이벤트도 선별적으로 캐치 가능
- 캡쳐링 단계의 이벤트를 캐치하려면 addEventListener의 3번째 인수로 true를 전달
- 3번째 인수를 생략하거나, false를 전달 => 타깃단계과 버블링 단계의 이벤트 캐치
