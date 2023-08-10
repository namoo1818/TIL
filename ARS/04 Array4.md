### 2023.08.10
# 2차원 배열의 접근
## 델타를 이용한 2차 배열 탐색 - 상하좌우 탐색
```java
// 상하좌우
dr = {-1,1,0,0}
dc = {0,0,-1,1}
```
```java
for (int d = 0; d < 4; d++) {
  int nr = r + dr[d]; 
  int nc = c + dc[d];

  if (nr >= 0 && nr < N && nc < 0 && nc < N) {
    System.out.println(arr[nr][nc]);
  }
}
```

## 전치 행렬
![전치행렬](https://github.com/namoo1818/SSAFY_Algorithm_Study/assets/50236187/20dd3fa2-5d51-49a8-b4f3-cee3032f8d7d)
```java
for (int i = 0; i < N; i++) {
  for (int j = i + 1; j < N; j++) {
    int tmp = arr[i][j];
    arr[i][j] = arr[j][i];
    arr[j][i] = tmp;
  }
}
```

# 연습 문제
## 달팽이 순회
```java
int num = 1;
int col = n;
int row = n-1;
int x = 0;
int y = 0;

// nxn 배열 생성
int[][] arr = new int[n][n];

// 달팽이 배열 만들기
while (num <= n * n) {
  for (int i = 0; i < col; i++) {
    if (arr[x][y] == 0) {
      arr[x][y++] = num++;
    }
  }
  col--; x++; y--;
  for (int i = 0; i < row; i++) {
    if (arr[x][y] == 0) {
      arr[x++][y] = num++;
    }
  }
  row--; x--; y--;
  for (int i = 0; i < col; i++) {
    if (arr[x][y] == 0) {
      arr[x][y--] = num++;
    }
  }
  col--; x--; y++;
  for (int i = 0; i < row; i++) {
    if (arr[x][y] == 0) {
      arr[x--][y] = num++;
    }
  }
  row--; x++; y++;
}
```
## 사과 나무 영양분 구하기
```java
// 입력
1
5
1 1 1 1 1
1 1 1 2 2 
1 1 1 2 1 
1 9 1 1 1 
1 1 1 1 1
```
```java
int[] dr = { -1, 1, 0, 0 };
int[] dc = { 0, 0, -1, 1 };

for (int i = 0; i < N; i++) {
  for (int j = 0; j < N; j++) {

    int sum = farm[i][j]; 

    for (int d = 0; d < 4; d++) {
      int nr = i + dr[d];
      int nc = j + dc[d];

      if (nr >= 0 && nr < N && nc >= 0 && nc < N) {
        sum += farm[nr][nc];
      }

      ans = Math.max(ans, sum);

    }
  }
}
```
