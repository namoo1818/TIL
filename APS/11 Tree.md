### 2023.08.23
# 트리 Tree
- 비선형 구조
- 원소들 간에 1:N 관계를 가지는 자료구조
- 원소들 간에 계층관계를 가지는 계층형 자료구조
- 상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무)모양의 구조
- 한 개 이상의 노드로 이루어진 유한 집합
- 루트(root) : 최상위 노드
- 나머지 노드들은 n개의 분리 집합 T1, ..., TN으로 분리될 수 있다. 이는 각각 하나의 트리가 되며(재귀적 정의) 루트의 부 트리(subtree)라고 한다.  
![트리](https://github.com/namoo1818/Baekjoon/assets/50236187/e8f27ae7-f138-45d9-863d-c5df22c9e358)  

### 노드(node)
> 트리의 원소
- 트리 T의 노드 : A, B, C, D, E, F, G, H, I, J, K
### 간선(edge)
> 노드를 연결하는 선, 부모 노드와 자식 노드를 연결
### 루트 노드(root node)
> 트리의 시작 노드
- 트리 T의 루트 노드 : A
### 형제 노드(sibling node)
> 같은 부모 노드의 자식 노드들
- H의 형제 노드 : I, J
### 조상 노드
> 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
- K의 조상 노드 : F, B, A
### 서브 트리(subtree)
> 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
### 자손 노드
> 서브 트리에 있는 하위 레벨의 노드들
- B의 자손 노드 : E, F, K
### 차수(degree)
- 노드의 차수 : 노드에 연결된 자식 노드의 수
- B의 차수 = 2, C의 차수 = 1
- 트리의 차수 : 트리에 있는 노드의 차수 중에서 가장 큰 값
- 트리 T의 차수 = 3
- 단말 노드(리프 노드) : 차수가 0인 노드. 즉, 자식 노드가 없는 노드
### 높이
- 노드의 높이 : 루트에서 노드에 이르는 간선의 수. 노드의 레벨
- B의 높이 = 1, F의 높이 = 2
- 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값. 최대 레벨
- 트리T의 높이 = 3  
![트리레벨](https://github.com/namoo1818/Baekjoon/assets/50236187/8db0c39a-922a-4887-b9e0-1ae119179e20)  

# 이진 트리
- 모든 노드들이 2개의 서브 트리를 갖는 특별한 형태의 트리
- 각 노드가 자식 노드를 최대한 2개까지만 가질 수 있는 트리
- 왼쪽 자식 노드(left child node), 오른쪽 자식 노드(right child node)
- 높이가 h인 이진 트리가 가질 수 있는 노드의 최소 개수는 (h+1)개가 되며, 최대 개수는 $(2^{h+1}-1)$개가 된다.  
![이진트리](https://github.com/namoo1818/Baekjoon/assets/50236187/441bb8e0-e159-4ae4-89e1-0eea4c8ef4df)

# 포화 이진 트리(Perfect Binary Tree)
- 모든 레벨에 노드가 포화상태로 차 있는 이진 트리
- 높이가 h일 때, 최대의 노드 개수인 $(2^{h+1}-1)$의 노드를 가진 이진 트리
- 높이가 3이면 노드 개수는 $2^{3+1}-1=15$개
- 루트를 1번으로 하여 $2^{h+1}-1$까지 정해진 위치에 대한 노드 번호를 가짐  
![포화이진트리](https://github.com/namoo1818/Baekjoon/assets/50236187/afd9c1c4-2794-42c9-a8f6-1b200e84a774)

# 정 이진 트리(Full Binary Tree)
- 자식이 0 또는 2개만 있는 노드들이 모여있는 트리  
![정이진트리](https://github.com/namoo1818/Baekjoon/assets/50236187/09d9dedc-0d3b-455a-84ef-c0d747639583)  

# ⭐완전 이진 트리(Complete Binary Tree)
- 높이가 h이고 노드 수가 n개일 때 (단, $h+1<=n<2^{h+1}-1$), 포화 이진 트리의 노드 번호 1번부터 n번까지 빈 자리가 없는 이진 트리
- 예) 노드가 10개인 완전 이진 트리  
![완전이진트리](https://github.com/namoo1818/Baekjoon/assets/50236187/a85904f9-5b8e-4791-a2a9-c180d67e3301)

# 편향 이진 트리(Skewed Binary Tree)
- 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리  
![편향이진트리](https://github.com/namoo1818/Baekjoon/assets/50236187/d19cee06-a0eb-4817-882b-f598763f4c99)

# 배열을 이용한 이진 트리의 표현
- **루트 번호를 1로 함**
- 레벨 n에 있는 노드에 대하여 왼쪽부터 오른쪽으로 $2^n$부터 $2^{n+1}-1$까지 번호를 차례로 부여
-  노드 번호를 배열의 인덱스로 사용
### 성질
> 배열을 통한 이진 트리라서 가능    
- 노드 번호가 i인 노드의 부모 노드 번호? [i/2]
- 노드 번호가 i인 노드의 왼쪽 자식 노드 번호? 2*i
- 노드 번호가 i인 노드의 오른쪽 자식 노드 번호? 2*i+1
- 레벨 n의 노드 번호 시작 번호는? $2^n$
- 높이가 h인 이진 트리를 위한 배열의 크기는?
$1+2+4+8+...+2^i=\sum{}^{} 2^{h+1}-1$  

### 단점
- 편향 이진 트리의 경우에 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생
- 트리의 중간에 새로운 노드를 삽입하거나 기존의 노드를 삭제할 경우 배열의 크기 변경 어려워 비효율적
![배열트리](https://github.com/namoo1818/Baekjoon/assets/50236187/1930217e-2cdb-4640-967b-5603d5786b11)

# 연결리스트를 이용한 이진 트리의 표현
- 이진 트리의 모든 노드는 최대 2개의 자식 노드를 가지므로 일정한 구조의 단순 연결 리스트 노드를 사용하여 구현  
![연결리스트트리](https://github.com/namoo1818/Baekjoon/assets/50236187/5c5f7115-f2b6-4cab-8c64-6dc86dff94d0)  
![완전이진트리연결리스트](https://github.com/namoo1818/Baekjoon/assets/50236187/f951e3e3-e337-4fb8-8234-7e1af27c1f0f)  

# 순회(traversal)
> 트리의 노드들을 체계적으로 방문하는 것   
![순회트리](https://github.com/namoo1818/Baekjoon/assets/50236187/5be1dfee-d841-42f8-98f8-f0a7d8e66613)  

## 전위 순회(preorder traversal) : VLR(부모 노드 방문-왼쪽 자식 노드-오른쪽 자식 노드)
방문 순서 : A B D E H I C F G
```java
public static void preorder(int i) {
  if(i < N) {
    if(arr[i] != ' ')
      System.out.print(arr[i]+" "); //V
    preorder(i*2);   //L
    preorder(i*2+1); //R
  }
}
```
## 중위 순회(inorder traversal) : LVR
방문 순서 : D B H E I A F C G
```java
public static void inorder(int i) {
  if(i < N) {
    inorder(i*2);   //L
    if(arr[i] != ' ')
      System.out.print(arr[i]+" "); //V
    inorder(i*2+1); //R
  }
}
```
## 후위 순회(postorder traversal) : LRV
방문 순서 : D H I E B F G C A
```java
public static void postorder(int i) {
  if(i < N) {
    postorder(i*2);   //L
    postorder(i*2+1); //R
    if(arr[i] != ' ')
      System.out.print(arr[i]+" "); //V
  }
}
```
