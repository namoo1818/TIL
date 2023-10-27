### 2023.10.27
- #port
- #server.port = 80
- 기본 포트: url에서 포트번호가 뜨지 않는다
- #context-path
#server.servlet.context-path=/board

.paths(PathSelectors.ant("/api*/**"))
ant 표현에 대해 한 번 생각해봐



-proxy : 대행자, 핵심 관심사항(실제기능) 앞뒤로 기타업무가 있을 수 있따 원래 같았으면 기타업무는 공통관심사항이다. 
너무 많아지니까 crosscutting

커다란 프록시를 만들어서 실행

핵심관심사항 전에 before
핵심관심사항이 완벽히 끝난 후에 after
핵심관심사항이 끝났을 떄 after-returnning
기타업무를 하다가 팡 터짐 after-throwing

xml/annotation 방식으로 해봤다

execution
around라는 걸로 얘기 해보기도 했다

mvc: **디패서**
