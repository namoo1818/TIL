### 2023.08.01
# 크기 단위
- 길이 값(length) : (절대단위) px, cm, mm, in / (상대단위) em, rem 등의 길이 단위 사용
### em: 부모엘리먼트의 font-size의 배수  
- 유지보수가 쉽다.  
- 예측이 쉽다.  
- 전체적인 틀을 잡을 때
### rem: html의 font-size의 배수, html의 기본적인 font-size은 16px   
- 세부적으로 조정할 때
### em과 rem은 반응형 디자인을 위해 사용
- 백분율(%) : 상위 block에 대한 백분율의 단위, 상위 block 크기가 바뀌면 자신의 크기도 자동으로 변경
- auto(width): 100%, 자신의 상위 block이 허용하는 width 크기만큼 채운다.
- auto(height): 0%, 높이를 결정하는 요인은 block box 속의 내용물의 크기
# 색상 단위
![ex_screenshot](/images/색상단위.PNG)
# font
![ex_screenshot](/images/font.PNG)
# Text
![ex_screenshot](/images/text.PNG)
# background
![ex_screenshot](/images/background.PNG)
# (매우 중요)box model
- 모든 HTML 요소는 box 형태로 되어 있음.
![ex_screenshot](/images/box_model.PNG)
## box model - margin
![ex_screenshot](/images/margin.PNG)
- 마진상쇄 현상 : 두 box가 있을 때 마진이 겹쳐질 수 있다. 상대방의 위치, 마진 고려 x
## box model - padding
![ex_screenshot](/images/padding.PNG)
## box model - border
![ex_screenshot](/images/border.PNG)
## box-sizing
![ex_screenshot](/images/box-sizing.PNG)
# display : block
- 줄 바꿈이 일어나는 요소
- 화면 크기 전체의 가로 폭을 차지
- 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
- 대표적인 블록 레벨 요소 : div, ul, ol, li, p, hr, form, ...
# display : inline
- 줄 바꿈이 일어나지 않는 행의 일부 요소
- content 너비만큼 가로 폭을 차지
- width, height, margin-top, margin-bottom을 지정할 수 없음
- 상하 여백은 line-height로 지정
- 대표적인 인라인 레벨 요소 : span, a, img, input, label, b, e, i, strong
# display : inline-block
- block과 inline 레벨 요소의 특징을 모두 갖는다
- inline처럼 한줄에 표시 가능
- block처럼 width, height, margin 속성 지정 가능
# display : none
- 해당 요소를 화면에 표시하지 않는다.(공간 x, 화면 x)
- visibility: hidden은 해당 요소(공간 o, 화면 x)
# position
- static(기본) -> 일반적인 내용물의 흐름, 상단, 좌측에서의 거리를 지정할 수 없다
- relative -> HTML 문서에서의 일반적인 내용물의 흐름을 말하지만, top, left 거리를 지정
- absolute -> 자신의 상위 box 속에서의 top, left, right, bottom 등의 절대적인 위치를 지정
- fixed -> 스크롤(scroll)이 일어나도 항상 화면상의 지정된 위치에 있다
# float
- float 속성은 박스를 어느 위치에 배치할 것인지를 결정하기 위해 사용
- none: 기본값
- left: 요소를 왼쪽으로 띄움
- right: 요소를 오른쪽으로 띄움
# clear 
- float 속성이 가지고 있는 값을 초기화 하기 위해 사용
- left, right: 각각의 속성 값을 취소할 수 있다
- both: 양쪽의 float 속성 값을 취소할 수 있다
- none: 기본값

# (시험 출제)flexbox
- Flexible Box module은 인터페이스 내의 아이템 간 공간 배분과 강력한 정렬 기능을 제공하기 위한 1차원 레이아웃 모델로 설계
![ex_screenshot](/images/flexbox.png)
## 주요 개념
- Main Axios(주축), Cross Axios(교차축)
- 시작선(start), 끝선(end)
- Container와 item

## Flex Container
- display 속성을 이용하여 container를 생성
- display flex; -> block 성격의 container
- display: inline-flex; -> inline 성격의 container
![ex_screenshot](/images/flex_container.PNG)

## Flex Item
![ex_screenshot](/images/flex_item.PNG)

- align-items : 교차축에 대한 정렬, 한줄일 때
- align-content : 여러 줄일 때
- align-items와 align-content 사이에 충돌이 생길 수 있다

## flex-basis
- 아이템 크기 지정

## flex-grow
- 팽창, 기본(0), 음수 불가능, 양수 가능
- 여유 공간에 대한 지분
- 여유 공간이 있을 때 늘어난다
## flex-shrink
- 수축, 기본(1), 음수 불가능, 양수 가능
