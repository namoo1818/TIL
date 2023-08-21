### 2023.08.21
# 원형 큐의 구조
- 선형큐의 문제점 : 잘못된 포화 인식 => 해결방법 : 앞으로 당기기, 원형큐
- 초기 공백 상태  
> front = rear = 0
- Index의 순환  
> front와 rear의 위치가 배열의 마지막 인덱스인 n-1를 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동 (나머지연산 이용)
- front 변수
> 공백 상태와 포화 상태를 구분을 쉽게 하기 위해 front가 있는 자리는 사용하지 않고 항상 빈자리로 둠  
- 삽입 위치 및 삭제 위치
  |  | 삽입 위치 | 삭제 위치 |
  |---|---|---|
  |선형큐| rear = rear + 1 | front = front + 1 |
  |원형큐| rear = (rear+1)%n | front = (front+1)%n |

- 원형큐에서 공간 하나는 공백상태와 포화상태 구분을 위해 비워둔다.
- 포화 상태  
> rear == (front+1) % 크기

```java
public static String[] queue = new String[5]; 
public static int size = queue.length;
public static int front = 0, rear = 0;

public static boolean isEmpty() {
		return front == rear;
	}

	// 포화상태 
	// rear에서 한칸 더 진행한 곳이 front가 가리키는 곳이라면 포화상태
	public static boolean isFull() {
		return front == (rear+1)%size;
	}

	// 삽입 : boolean / 자료형 / void
	public static void enQueue(String item) {
		// 배열로 만들었을 때 (연결리스트로 만들었다면 생략 가능)
		if (isFull()) {
			System.out.println("가득 차서 더 이상 넣을 수 없다!");
			return;
		}
		// 넣는 행위를 하려면
		rear = (rear+1)%size;
		queue[rear] = item;
	}

	// 삭제
	public static String deQueue() {
		// 공백쳌은 꼭 필요
		if (isEmpty()) {
			System.out.println("공백상태 입니다.");
			return null;
		}
		front = (front+1)%size;
		return queue[front];
	}
```

# 우선순위 큐
- 우선순위를 가진 항목들을 저장하는 큐
- FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 된다

## 우선순위 큐의 구현
- 배열 이용한 우선순위 큐
- 리스트를 이용한 우선순위 큐

## 비교 기준
Comparable 또는 Comparator 사용

## 우선순위 큐의 기본 연산
- 삽입 enQueue 
- 삭제 deQueue : 우선순위에 맞게 재배치

## 배열을 이용한 우선순위 큐
- 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입하는 구조
- 가장 앞에 최고 우선순위의 원소가 위치하게 됨
### 문제점
- 배열을 사용하므로, 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생함
- 이에 소요되는 시간이나 메모리 낭비가 큼

# 삽입 정렬 Insertion Sort  
> 자료 배열의 모든 원소들을 앞에서부터 차례대로 이미 정렬된 부분과 비교하여, 자신의 위치를 찾아냄으로써 정렬을 완성한다.  
- 평균 시간복잡도 O($n^2$)
- 최선 시간복잡도 O($n$) `이미 정렬된 경우`
```java
public class InsertionSort {
	public static void main(String[] args) {
		int[] data = { 69, 10, 30, 2, 16, 8, 31, 22 };
		for (int i = 1; i < data.length; i++) {
			int key = data[i]; 
			for (int j = i - 1; j >= 0; j++) {
				data[j+1] = data[j];		
			} 
		}
	}
}
```


![정렬정리](https://github.com/namoo1818/Baekjoon/assets/50236187/8dae2aa0-3cd8-44da-bb94-fcb2e3f9d962)
