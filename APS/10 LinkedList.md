### 2023.08.22
# 연결 리스트
- 자료의 논리적인 순서와 메모리 상의 물리적인 순서가 일치하지 않고, 개별적으로 위치하고 있는 원소의 주소를 연결하여 하나의 전체적인 자료구조를 이룬다
- 링크를 통해 원소에 접근하므로, 리스트에서처럼 물리적인 순서를 맞추기 위한 작업이 필요하지 않다.
- 자료구조의 크기를 동적으로 조정할 수 있어, 메모리의 효율적인 사용이 가능하다
- Node : **데이터**와 **주소**를 가지고 있다.

# 노드
- 연결 리스트에서 하나의 원소에 필요한 데이터를 갖고 있는 자료단위
- 구성요소
> 1) 데이터 필드
> - 원소의 값을 저장하는 자료구조
> - 저장할 원소의 종류나 크기에 따라 구조를 정의하여 사용 
> 2) 링크 필드
> - 다음 노드의 주소를 저장하는 자료구조
```java
class Node {
  // 데이터 필드
  클래스
  String
  int
  // 링크 필드(주소)
  Node link (주소값)
}
```
![노드](https://github.com/namoo1818/Baekjoon/assets/50236187/798862d4-cac5-4a01-9aff-ff5355c0a2d9)  


# 헤드
- 시작 주소
- 헤드의 자료형은 노드
- 리스트의 처음 노드를 가리키는 레퍼런스

# 단순 연결 리스트 Singly Linked List
- 노드가 하나의 링크 필드에 의해 다음 노드와 연결되는 구조
- 헤드가 가장 앞의 노드를 가리키고, 링크 필드가 연속적으로 다음 노드를 가리킨다.
- 최종적으로 NULL을 가리키는 노드가 리스트의 가장 마지막 노드다.
- 노드를 삽입 또는 삭제할 때 **순서가 중요하다**
- 노드를 삭제하면 가비지 컬렉터가 냠냠한다  
![단순연결리스트](https://github.com/namoo1818/Baekjoon/assets/50236187/1fe549cc-3520-43b6-b7e8-85e04d733e63)

```java
// 첫번째 위치에 원소 삽입
public void addFirst(String data) {
  // 노드를 생성한다.
  Node node = new Node(data); // 생성자를 만들어 놓았으니 인스턴스 생성 가능
  // 순서중요
  node.link = head;
  head = node; // head가 첫번째 원소를 가리키는 거니까 넣어
  size++;
}

// 마지막 위치에 원소 삽입
public void addLast(String data) {
  // head가 null이라는건? size가 0인 공백리스트라는 의미
//		if(head==null)
  if(size==0) {
    addFirst(data);
    return;
  }
  
  Node node = new Node(data);
  // 마지막 노드를 찾아가자
  Node curr = head;
  while(curr.link!=null) {
    curr = curr.link;
  }
  curr.link = node;
  size++;
}

// 중간 원소 삽입
public void add(int idx, String data) {
  if(idx<0 || idx>size) {
    System.out.println("유효하지 않은 인덱스를 작성했다.");
    return;
  }
  if(idx==0) {
    addFirst(data);
    return;
  }
  if(idx==size) {
    addLast(data);
    return;
  }
  Node pre = get(idx-1); // 조회 함수를 만들어 두었으니까 이전 노드를 찾는 것은 매우 쉽다
  
  Node node = new Node(data);
  node.link = pre.link;
  pre.link = node;
  size++;
}
```

# 이중 연결 리스트 Doubly Linked List  
![이중연결리스트](https://github.com/namoo1818/Baekjoon/assets/50236187/30b62526-8fdc-4b6e-8b6a-d671a04fef58)  

# 리스트를 이용한 스택
- 스택의 원소 : 리스트의 노드
- Push : 리스트의 마지막에 노드 삽입
- Pop : 리스트의 마지막 노드 반환/삭제
- 변수 top : 리스트의 마지막 노드를 가리키는 변수
- top의 초기 상태 : null

# 연결 큐 Linked List
- 큐의 원소 : 단순 연결 리스트의 노드
- 큐의 원소 순서 : 노드의 연결 순서. 링크로 연결되어 있음
- front : 첫 번째 노드를 가리키는 링크
- rear : 마지막 노드를 가리키는 링크
- 초기 상태 : front = rear = null
- 공백 상태 : front = rear = null

# 배열을 이용한 우선순위 큐
![배열을이용한우선순위큐](https://github.com/namoo1818/Baekjoon/assets/50236187/15c0e1e4-4a8c-4df4-b7e5-d1cd21802e07)

# 리스트를 이용한 우선순위 큐
![리스트를이용한우선순위큐](https://github.com/namoo1818/Baekjoon/assets/50236187/e48ac734-9067-45c9-8423-76ab62b6b4a1)
