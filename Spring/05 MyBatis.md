### 2023.10.16
environment, mapper는 필수 작성

configuration는 작성 순서가 있다
(MyBatis 사용자 가이드 참고)
- configuration
  - properties
  - settings
  - typeAliases
  - typeHandlers
  - objectFactory
  - plugins
- environments
  - environment
    - transactionManager
    - dataSource
  - databaseIdProvider
  - mappers
