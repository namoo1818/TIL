### 2023.08.08
# 순차 검색(Sequential Search)
일렬로 되어 있는 자료를 순서대로 검색하는 방법
- 가장 간단하고 직관적
- 시간복잡도 $O(n)$
```java
int idx = 0;
while (idx < arr.length) {
  if (arr[idx] == key) {
    return true;
  }
  idx++;
}
return false;
```
# 이진 탐색(Binary Search)
![BinarySearch](https://github.com/namoo1818/TIL/assets/50236187/eb9d2964-95c2-4575-9a04-8786d9d8f1b7)  
자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색 위치를 결정하고 검색을 계속 진행하는 방법
- 정렬된 배열만 가능
- 시간복잡도 $O(logN)$  
```java
int start = 0;
int end = arr.length - 1;
while (start <= end) {
  int mid = (start + end) / 2;
  if (arr[mid] == key)
    return true;
  // 왼쪽으로 이동
  else if (arr[mid] > key)
    end = mid - 1;
  // 오른쪽으로 이동
  else
    start = mid + 1;
}
return false;
```
참고 : https://blog.penjee.com/binary-vs-linear-search-animated-gifs/

# 선택 정렬(Selection Sort)
![SelectionSort](https://github.com/namoo1818/TIL/assets/50236187/023a5426-7ed9-4eeb-8e46-52a1a2bdfc88)  
해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘
- 제자리 정렬(in-place sorting) 알고리즘의 하나
- 시간복잡도 $O(n^2)$
```java
for(int i = 0; i<N-1;i++){
  int minIdx = i; 
  for(int j = i+1;j<N;j++) {
    if(nums[j] < nums[minIdx]) {
      minIdx = j;
    }	
  }
  int tmp = nums[i];
  nums[i] = nums[minIdx];
  nums[minIdx] = tmp;
}
```
# 계수 정렬(Counting Sort)
<img src="https://github.com/namoo1818/TIL/assets/50236187/f8a3e7f4-54e5-4548-8cbd-8aef92aeb711"  width="500">   

항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘    
- 정수만 가능
- 값의 범위가 너무 크면 안됨
- 안정정렬 : 같은 값을 가지는 원소들이 정렬 후에도 정렬 전과 같은 순서를 가짐.
- 시간복잡도 $O(n)$
```java
int[] arr = { 8, 8, 24, 12, 19, 3, 45, 60 };
int N = arr.length;

// 1. 데이터 중 가장 큰 값을 알고 있어야 한다.
int K = -1;
for (int i = 0; i < N; i++) {
  if (K < arr[i])
    K = arr[i];
} // 최대값을 찾는 for문

int[] count = new int[K + 1]; // 0~60: 61칸

// 2. 개수 카운팅
for (int i = 0; i < N; i++) {
  count[arr[i]]++; // 해당 값을 인덱스로 하여 카운트를 증가시킴
}

// 3. 누적합을 구한다. (얘를 구함으로써 들어갈 수 있는 위치가 결정되고 안정정렬이 가능하다)
for (int i = 1; i < count.length; i++) {
  count[i] += count[i - 1];
}

// 4. 원본배열의 뒤에서부터 순회를 하며 정렬된 배열에 차곡차곡 저장한다.
int[] sortArr = new int[N];
for (int i = N - 1; i >= 0; i--) {
  // 지금 저장하고 싶은 값 : arr[i]
  // 저장하고 싶은 위치 : count[arr[i]]-1 -> 하고나서 한번 더 count[arr[i]]--;
  // --count[arr[i]]

  sortArr[--count[arr[i]]] = arr[i];
}
```
# 정렬 알고리즘 비교
![정렬알고리즘비교](https://github.com/namoo1818/TIL/assets/50236187/88845a7b-c8c4-4cc3-82f6-e2f4581099f9)  
