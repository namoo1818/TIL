### 2024.01.03

# Issue Tracking
- Jira는 이슈 트랙킹 툴이다
- Project Management : 커뮤니케이션, 계획, 컨트롤, 리스크 관리

# Agile
- 공정과 도구보다 개인과 상호작용
- 포괄적인 문서보다 작동하는 소프트웨어
- 계약 협상보다 고객과의 협력
- 계획을 따르기보다 변화에 대응

![agile-scrum-vs-agile-kanban5](https://github.com/namoo1818/TIL/assets/50236187/19b22fe7-962b-42bf-8348-ce9c2739f27f)

## 방법론1 : Scrum
- 이슈를 백로그 공간에 담아둠
- 2주동안 해당 기간에 정한 스크린트(이슈 처리)와 회고 진행

## 방법론2 : Kanban

# DevOps
- DevOps 자동화 툴

# SRE

# 사용법
- Issue type
  - `Story` : 유저스토리, 사용자가 어떤 동작을 처리하는지
  - `Epic` : 스토리의 하나의 큰 묶음
  - Bug : 버그
  - Task : 그 외  
- Summary : 이슈 제목
- Components : 진행 단위, 소그룹 단위
- Label : 해시태그
- Story point estimate : 이슈 난이도

# JQL
> Jirs Query Language
- Jira Issua를 구조적으로 검색하기 위해 제공하는 언어
- SQL(Standard Query Language)과 비슷한 문법
- Jira의 각 필드들에 맞는 특수한 예약어들을 제공
- 쌓인 Issue들을 재가공해 유의미한 데이터를 도출해 내는데 활용(Gadget, Agile Board 등)

# JQL Functions
- endOfDay(), startOfDay()
- endOfWeek() (Saturday), startOfWeek() (Sunday)
- endOfMonth(), startOfMonth(), endOfYear(), startOfYear()
- currentUser(): 지금 로그인한 유저 확인
