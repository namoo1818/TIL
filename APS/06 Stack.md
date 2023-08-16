### 2023.08.16
# Stack
> 물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조  
- **선형 구조, 후입선출(LIFO)**  
`선형구조 : 자료 간의 관계가 1:1`  
`비선형구조 : 자료 간의 관계가 1:N (예:트리)`  
- 프링글스통, 접시 더미를 생각하면 된다
- 깊이 우선 탐색 DFS에서 사용
- 저장소 자체를 스택이라 부르기도 한다
- 스택에서 마지막으로 삽입된 원소의 위치를 top이라 부른다
- push(삽입), pop(삭제), isEmpty(공백확인), peek(top에 있는 원소 반환)
- 장점 : 1차원 배열일 경우 구현이 용이하다
- 단점 : 스택의 크기를 변경하기 어렵다 → 동적 할당으로 스택 구현하면 해결

## 구현
```java
// 삽입
public static void push(int value) {
  if (isFull()) {
    System.out.println("못넣음");
    return;
  }
  stack[++top] = value;
}

// 삭제
public static int pop() {
  if (isEmpty()) {
    System.out.println("못뺌");
    return -1; // 자료 중에 -1이 있을수도 있으니까 이건 주의 요망
  }
  // top 위치만 옮긴다
  return stack[top--];
}

// 포화상태 체크
public static boolean isFull() {
  return top == stack.length - 1;
}

// 공백상태 체크
public static boolean isEmpty() {
  return top == -1;
}
```
