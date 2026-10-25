# BufferedReader와 BufferedWriter

### BufferedReader이란
- Scanner와 달리 Enter만을 경계로 인식하고 받은 데이터가 String으로 고정된(Scanner은 space와enter둘다 경계로 인식함).
- BufferedReader는 한 번에 큰 덩어리(8192자)를 메모리 버퍼로 읽어 두고 거기서 줄 단위로 꺼내 쓴다. Scanner도 내부 버퍼(1024자)로 읽지만, 토큰마다 정규식으로 경계를 찾고 타입을 검사하는 파싱 비용이 커서 느리다. 그래서 입력이 많을수록 BufferedReader가 더 빠르다.
  
<br>

### BufferedReader사용법
```java
BufferedReader br=new BufferedReader(new InputStreamReader(system.in));//선언
String s= br.readLine();//String형태로 입력
int i=Integer.parseInt(br.readLine());
```
-BufferedReader의 경우 입력을 String형으로 입력받기 떄문에 반드시 원하는 자료구조로 변경해야한다
```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));//
StringTokenizer st = new StringTokenizer(br.readLine());br.readLine로 한줄을 입력받은 다음 공백을 기준으로 토큰을 나눠서 st에 담음
int a=Integer.parseInt(st.nextToken());//토큰을 int형으로 저장
int n=Integer.parseInt(st.nextToekn());
```
-이방법 경우 공백을 경계로 두고 입력을 받을떄 사용한다

###BufferedWriter
- BufferedWriter은 버퍼에 쌓아두었다가 출력하는 형태이다
- System.out.print()와 달리 호출마다 작업이 일어나지 않고 버퍼에 쌓아두었다가 한꺼번에 내보내서 출력횟수가 현저히 적다
```java
BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(System.out));

bw.write("hello");//버퍼에 "hello"저장

bw.close(); //버퍼안에있는 "hello"출력 및 종료
```
### SCanner와 BufferedWriter 속도차이 실험
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        // 1부터 100만까지 적힌 입력 데이터 만들기
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= 1000000; i++) sb.append(i).append("\n");
        String input = sb.toString();

        // Scanner로 읽기
        long start = System.currentTimeMillis();
        Scanner sc = new Scanner(input);
        for (int i = 0; i < 1000000; i++) sc.nextInt();
        System.out.println("Scanner: " + (System.currentTimeMillis() - start) + "ms");

        // BufferedReader로 읽기
        start = System.currentTimeMillis();
        BufferedReader br = new BufferedReader(new StringReader(input));
        for (int i = 0; i < 1000000; i++) Integer.parseInt(br.readLine());
        System.out.println("BufferedReader: " + (System.currentTimeMillis() - start) + "ms");
    }
}
```
- 결과값:Scanner:3997ms BufferedReader: 342ms
### 정리 및 요약
-  한꺼번에 입력을 받아 버퍼로 읽어두고 BufferedWriter로 한꺼번에 출력 하므로 Scanner와 달리 많은 입력에서 훨씬 빠르다.
- 입력값이 적을떄는 차이가 별로 없지만 입력값이 많아질수록 차이가 많이 나기 때문에 입력의 크기를 보고 bufferedReader를 사용해야한다


