### 2023.07.12  
## <스타트 캠프 1일차>  
  
집에도 java 8버전을 깔자  
JDK : Java Development Kit 자바 개발에 필요한 모든 것이 들어있다  
JRE : Java Runtime Environment  
JVM : Java Virtual Machine  
  
ctrl + space : 자동완성   
ctrl + shift + f : 들여쓰기 자동정리

<br>  
변수 : 데이터를 담아두는 상자   
컴퓨터에서 실수 계산은 정확하지 않다.   

자료형 8가지 기억해 : 논리형 boolean / 문자형 char / 정수형 byte, short, int, long / 실수형 float, double  

논리형 연산자 &&, || 사용 시 단축평가에 유의하자  
단축평가란? A, B의 순서에 따라 컴퓨터의 퍼포먼스가 달라진다  
ex) A && B => A가 false면 B를 확인하지 않아도 된다  
　　A || B => A가 true면 B를 확인하지 않아도 된다  

if문은 무조건 검사한다. if-if문 코드(두 번 검사)와 if-else문 코드(한 번 검사)의 성능이 다르다.  
if-else if-else문 사용 시 순서가 중요하다! 

switch문 사용 예시 (break문이 없으면 계속 내려간다) 
1. 아래만 확인
2. 위아래 확인
3. 위아래 양옆 

switch (기능) {  
case 3   
 　(좌우)  
case 2  
 　(위)  
case 1  
 　(아래)  
 }


  반복문  
  1. for(초기식;조건식;증감식){실행문};   
     초기식과 증감식에는 comma(,)를 써서 변수 여러개를 쓸 수 있다. 조건식에서는 논리연산자(&&,||) 사용.    
     ex) for(int i=0, int j=1;i<10;i++,j+=2){ }    
     초기식, 조건식, 증감식은 각각 생략 가능하다. 세개 다 생략도 가능.(무한 반복문)   
     실행순서 : 1->2->4->3->2->4->3->...  
                        
  2. while(조건식){실행문};
  3. do{
     실행문
   }while(조건식);  
     do에 있는 실행문은 무조건 한 번 실행하고 조건식을 평가한다.

  4. 향상된 for문

