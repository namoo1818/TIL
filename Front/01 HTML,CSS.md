### 2023.07.21
# HTML
- Hyper Text Markup Language
- Hyper Text : 참조(링크)를 통해 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트
- Markup : 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어
- 웹페이지를 작성하기 위한 언어
- .html(확장자)를 가짐.
- 태그는 대소문자 구분이 없음.
- 엔터, 스페이스바, 탭이 적용되지 않음.
# 태그(Tag)
- HTML의 요소는 태그와 내용으로 구성
```html
<a href="https://edu.ssafy.com/">에듀싸피</a>
```
<a href="https://edu.ssafy.com/">에듀싸피</a>
- 시작태그 / 종료태그로 쌍을 이루거나 시작 tag만 존재하는 tag도 있다
- 각각의 시작태그는 속성과 속성값을 가질 수 있다
# 주석
- 주석의 내용은 브라우저에 출력이 되지 않음
- HTML tag의 내용을 설명하기 위한 용도로 사용
- \<!--주석 내용-->
# 기본 구조
- html: HTML 최상위 요소, 문서의 root -> head와 body로 구성
- head: 문서제목 문자코드(인코딩) 등 해당 문서에 대한 정보를 가지고 있고, 브라우저 화면 출력 x
- meta: 문서의 작성자, 날짜 등 본문에 나타나지 않는 일반 정보들
- body: 브라우저 화면에 나타나는 정보  
  id 속성을 이용하여 문서 내에세 tag 식별 가능 (중복 x)  
  class 속성을 이용하여 여러 tag에 공통적인 특성 부여 (중복 o)
```html
<!DOCTYPE html>
<html lang='en'>
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>

</body>
</html>
```
# 특수문자
|엔티티이름|화면출력|
|----------|--------|
|\&nbsp;   |&nbsp;  |
|\&lt;     |&lt;    |
|\&gt;     |&gt;    |
|\&gamp;   |&gamp;  |
|\&quot;   |&quot;  |
|\&copy;   |&copy;  |
|\&reg;    |&reg;   |

# Semantic tag
- 의미론적 요소를 잠은 태그의 등장

|태그이름|설명|
|----------|----------------------|
|\<header> |문서 전체나 섹션은 헤더 |
|\<nav>    |네비게이션             |
|\<aside>  |사이드에 위치한 공간    |
|\<section>|문서의 일반적인 구분    |
|\<article>|문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역|
|\<footer> |문서 전체나 섹션이 푸터 |
|\<h1>~\<h6>|6단계 구획 제목        |

- 코드의 가독성을 높이고 유지보수를 쉽게 함
![ex_screenshot](/images/Semantic_tag.PNG)

# Text content
- block

|태그이름|설명|
|---|---|
|\<blockquote>|긴 인용문, 주로 들여쓰기를 한 것으로 그려짐|
|\<hr>|구분선|
|\<pre>|공백, 줄바꿈 등 입력된 그대로 화면에 표시|
|\<p>|하나의 문단|
|\<ul>|정렬되지 않은 목록(번호 없는)|
|\<ol>|정렬된 목록(번호 있는)|
|\<div>|구문 컨텐츠를 위한 블록 컨테이너| 

### display는 inline과 block 로 이루어져 있다
- inline: 필요한 만큼만 차지
- block: 새로운 줄에서 시작, 그 한 줄을 다 차지

# Inline text semantics
![ex_screenshot](/images/Inline_test_semantics.PNG)

# Image & Multimedia
![ex_screenshot](/images/Image&Multimedia.PNG)

# Table content
![ex_screenshot](/images/table_content.PNG)

# (중요!)Forms
- 사용자로부터 데이터를 입력 받아 서버에서 처리하기 위한 용도로 사용
- 사용자가 작성한 데이터를 서버로 전송 (submit)
![ex_screenshot](/images/forms1.PNG)
![ex_screenshot](/images/forms2.PNG)

# input
- 요소의 동작은 type 속성에 따라 달라짐.
![ex_screenshot](/images/input.PNG)

# CSS
- Cascading Style Sheets (중요도 파악)
- HTML 문서를 화면에 표시하는 방식을 정의한 언어
- 웹 문서의 내용과 관계없이 디자인만 바꿀 수 있음
- 다양한 기기에 맞게 반응형으로 바뀌는 문서를 만들 수 있음
- 웹 브라우저 별 CSS3 지원

## 기본구조
![ex_screenshot](/images/css_기본구조.PNG)

## 적용 방법(External style sheet)
### 1. External style sheet
![ex_screenshot](/images/external_style_sheet.PNG)

## 2. Internal style sheet
- 파일 내에 스타일을 적용하는 방식  
- <style> 태그 사이에 CSS 규칙 작성  
- \<head> 안에 작성  
- 외부 스타일 시트보다 우선 적용  
![ex_screenshot](/images/Internal_style_sheet.PNG)![ex_screenshot](/images/내부_스타일_시트.PNG)

## 3. Inline sytle
- tag에서 style 속성을 사용하고 속성값으로 CSS 규칙 작성
- 스타일 적용 우선순위는 '인라인 -> 내부 스타일 시트 -> 외부 스타일 시트'순
![ex_screenshot](/images/Inline_style.PNG)

# CSS 선택자 (CSS Selector)
- HTML 문서에서 CSS 규칙을 적용할 요소를 정의
- 기본 선택자  
> \- 전체 선택자  
> \- 유형 선택자  
> \- 클래스 선택자  
> \- id 선택자  
> \- 특성 선택자  
- 그룹 선택자
- 결합자  
> \- 자손 결합자, 자식 결합자  
> \- 일반 형제 결합자, 인접 형제 결합자, 열 결합자  
- 의사 클래스/요소  
> \- 의사 클래스  
> \- 의사 요소  

### id와 class는 대소문자 구분을 한다.

## Universal selector(전체 선택자)
- HTML 문서 내 모든 element를 선택
- 사용법 -> *{style properties}

## Type selector(유형 선택자)
- 태그명을 이용하여 스타일을 적용할 태그를 선택
- HTML 내에서 주어진 유형의 모든 요소를 선택
- 사용법 -> element {style properties}

## Class selector(클래스 선택자)
- class 가 적용된 모든 태그를 선택
- HTML 내에서 동일한 클래스 명을 중복해서 사용가능
- 사용법 -> .class-name{style properties}

## ID selector(ID 선택자)
- id 특성 값을 비교하여, 동일한 id를 가진 태그를 선택
- HTML 내에서 주어진 ID를 가진 요소가 하나만 존재 해야함
- 사용법 -> #id-value{style properites}

## Selector list(선택자 목록)
- ,를 이용하여 선택자 그룹을 생성하는 방법
- 모든 일치하는 노드를 선택
- 사용법 -> element, element{style properties}

## Descendant combinator(자손 결합자)
- 첫 번째 요소의 자손인 노드를 선택
- 사용법 -> selector1 selector2{style properties}

## Child combinator(자식 결합자)
- 첫 번째 요소의 바로 아래 자식인 노드를 선택
- 사용법 -> selector1>selector2 {style properties}

## General sibling combinator(일반 형제 결합자)
- 첫 번째 요소를 뒤따르면서 같은 부모를 공유하는 두 번째 요소를 모두 선택
- 사용법 -> former-element~target-element{style properties}

## Adjacent sibling combinator(인접 형제 결합자)
- 첫 번째 요소의 바로 뒤에 위치하면서 같은 부모를 공유하는 두번째 요소 선택
- 사용법 -> former-element + target-element{style properties}

## 정리
> ### * => 전체
> ### element => 유형
> ### .calss-name => 클래스
> ### #id-value => ID
> ### A, B => 목록
> ### A B => 자손
> ### A > B => 자식
> ### A ~ B => 일반 형제
> ### A + B => 인접 형제

# 우선순위
- 같은 요소에 두 개 이상의 CSS 규칙이 적용된 경우  
  **마지막 규칙, 구체적인 규칙, !important 가 우선 적용**
- **우선순위 : 중요도(!important) > inline > id > class > 순서(나중부터)**
  
# 상속 (Inheritance)
- 부모 요소에 적용된 스타일이 자식 요소에게 상속이 될 수도 있고, 안 될 수도 있음
- 상속 되는 속성  
> \- 요소의 상속되는 속성에 값이 지정되지 않은 경우, 요소는 부모 요소의 해당 속성의 계산 값을 얻음.  
> \- 대표적인 예는 color 속성  
- 상속되지 않는 속성
> \- 요소의 상속되지 않는 속성에 어떤 값이 지정되지 않는 경우, 요소는 그 속성의 초기값을 얻음.  
> \- 대표적인 예는 border 속성
- 누가 상속 되는지 안 되는지는 도큐먼트를 확인해야함
