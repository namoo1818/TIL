### 2023.08.14
# 문자열
## 컴퓨터에서의 문자표현
> 각 문자에 대해서 대응되는 숫자를 정해 놓고 이것을 메모리에 저장하는 방법 사용
- 영어가 대소문자 합쳐서 52 이므로 6(64)비트면 모두 표현 가능 → 코드 체계
- 000000 -> 'a'
- 000001 -> 'b'

## ASCII
각 지역 별로 코드 체계가 달라서 서로간에 정보를 주고 받을 때 달리 해석한다는 문제 발생  
→ 표준안을 만들자!  
- 7bit 인코딩으로 128문자를 표현하며 33개의 출력 불가능한 제어 문자들과 공백을 비롯한 95개의 출력 가능한 문자들로 이루어져 있다
- 알아두면 편해요 : **0(48), A(65), a(97)**  
```java
int b = 'A';
System.out.println(b); // 65
```

## 확장 아스키
표준 문자 이외 악센트 문자, 도형 문자, 특수 문자, 특수 기호 등 부가적인 문자를 128개 추가할 수 있게 하는 부호  

## 유니코드
> 다국어 처리를 위한 표준
- 한글 코드체계 조합형, 완성형 두가지 중 완성형을 채택
- Character Set으로 분류 : UCS-2, UCS-4
- 유니코드 인코딩 : UTF-8, UTF-16, UTF-32

## Java에서의 문자열 처리
- String클래스 사용
```java
String str1 = "abc"; 
String str2 = new String("abc");

System.out.println(str1);
System.out.println(str2);

System.out.println(str1==str2); // false 주소비교라서
System.out.println(str1.equals(str2)); // true
```
- 문자열 처리에 필요한 연산을 연산자, 메소드 형태로 제공
> +, length(), replace(), split(), substring(), ...

## 문자열 뒤집기
```java
// 1. 거꾸로 읽기
char[] str = new char[text.length()];
for (int i = text.length() - 1, idx = 0; i >= 0; i--) {
  str[idx++] = text.charAt(i);
}
System.out.println(Arrays.toString(str));

// 2. swap 방식
char[] str2 = text.toCharArray();
int len = str2.length;

for (int i = 0; i < len / 2; i++) {
  char temp = str2[i];
  str2[i] = str2[len - 1 - i];
  str2[len - 1 - i] = temp;
}
System.out.println(Arrays.toString(str2));

// 3. StringBuilder / StringBuffer
StringBuilder sb = new StringBuilder();
sb.append(text);
sb.reverse();
System.out.println(sb);
```

## 문자열을 정수형으로
```java
public static int atoi(String text) {
  int value = 0;
  int digit = 0;
  for(int i = 0;i<text.length();i++) {
    char num = text.charAt(i); 
    if(num>='0' && num<='9') {
      digit = num - '0';
    } else {
      // 여기에 들어오면... 숫자가 아닌 이상한 것이 껴있다는 뜻
      // 버려
    }
    value = (value*10)+digit;
  }
  return value;
}
```
## 정수형을 문자형으로 
```java
public static String itoa(int value) {
  String text = "";
  if(value<0) {
    text += '-';
    value -= value*2;
  }
  int n = 1;
  while(value>=n) {
    n*=10;
  }
  while(n>1) {
    n/=10;
    int tmp = value/n;
    text += (char)(tmp+'0');
//			text += Integer.toString(tmp).charAt(0); // 이것도 가능
    value -= tmp*n;
  }
  return text;
}
```
## 패턴 매칭
- 본문 문자열에 찾으려는 문자 패턴이 있는지 탐색
- 우리는 브루트포스로 풀겠다(시간복잡도 O(MN))
```java
public static int bruteForceWhile(String t, String p) {
  int N = t.length();
  int M = p.length();
  
  int i = 0; // 본문의 인덱스
  int j = 0; // 패턴의 인덱스
  
  while(j<M && i<N) {
    if(t.charAt(i) != p.charAt(j)) {
      i -= j;
      j = -i;
    }
    i++;
    j++;
  }
  if(j==M)
    return i - M;
  return -1;
}
```
```java
public static int bruteForceFor(String t, String p) {
  int N = t.length(); // 본문의 길이
  int M = p.length(); // 패턴의 길이
  
  for(int i = 0; i< N+M; i++) {
    boolean flag = true;
    for(int j = 0; j<M;j++) {
      if(p.charAt(j)!=t.charAt(i+j)) {
        flag = false;
        break;
      }
    } 
    if(flag) {
      return 1;
    }
  }
  return -1; // 못 찾았을 경우 (없을 경우)
}
```
## 패턴 매칭 - 보이어 무어 알고리즘
- 오른쪽에서 왼쪽으로 비교
- 대부분의 상용 소프트웨어에서 채택하고 있는 알고리즘
- 문자 패턴의 오른쪽 끝에 있는 문자가 불일치하고 이 문자가 패턴 내에 존재하지 않는 경우, 이동거리는 무려 패턴의 길이!  
![보이어-무어-알고리즘](https://github.com/namoo1818/TIL/assets/50236187/6158064e-8b30-4e6e-be00-64680c56eb27)
