### 2023.08.09
# 완전 검색(Exhaustive Search)
모든 경우의 수를 확인해서 답을 찾는 기법  
Brute-force 또는 Generate-and-Test 기법이라고도 불림

# 순열(Permutation)
- 서로 다른 n개 중 r개를 뽑아서 한 줄로 나열하는 것
- ${}_n \mathrm{ P }_k = n * (n+1) * (n+2) * ... * (n-r+1) = {n! \over (n-r)!} $
- ${}_n \mathrm{ P }_n = n * (n+1) * (n+2) * ... * 2 * 1 = n! $

# 탐욕(Greedy) 알고리즘
- 매 선택에서 지금 이 순간 당장 최적인 답을 선택하여 적합한 결과를 도출하는 기법
- 근시안적인 방법

# 2차원 배열
- 행의 길이 n, 열의 길이 m인 2차원 배열
- int[][] twoDimArr = new int[n][m]

## 배열 순회
- n x m 배열의 n*m개의 모든 원소를 빠짐 없이 조사하는 방법

## 행 우선 순회
```
int i; // 행의 좌표
int j; // 열의 좌표

for i from 0 to n-1
  for j from 0 to m-1
    Array[i][j] // 필요한 연산 수행
```
