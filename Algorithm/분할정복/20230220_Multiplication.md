# 백준 1629 - 곱셈
https://www.acmicpc.net/problem/2630

### 이 문제를 풀기 위한 과정
전형적인 분할정복 문제이다. 

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static int A, B, C;
	static int answer = 0;

	public static void main(String args[]) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());

		A = Integer.parseInt(st.nextToken());
		B = Integer.parseInt(st.nextToken());
		C = Integer.parseInt(st.nextToken());

		long answer = solution(A, B);
		
		System.out.println(answer);
	}

	static long solution(int x, int n) {
		if (n == 1) {
			return x % C;
		}
		long y = solution(x, n / 2);
		return n % 2 == 0 ? (y * y) % C : ((y * y) % C * x) % C;
	}
}
```

# 23.02.20(월)
* 
