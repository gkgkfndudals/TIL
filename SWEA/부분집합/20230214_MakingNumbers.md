# SWEA 4008 - 숫자 만들기
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeRZV6kBUDFAVH

### 이 문제를 풀기 위한 과정
이 문제는 재귀로 풀 수 있다.

CODE1
```java
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution {
	static int[] oper;
	static int[] arr;
	static int answer;
	static int operCnt;
	static int maxVal;
	static int minVal;

	public static void main(String args[]) throws Exception {
		
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for (int test_case = 1; test_case <= T; test_case++) {
			answer = 0;
			operCnt = 0;
			maxVal = Integer.MIN_VALUE;
			minVal = Integer.MAX_VALUE;
			int N = Integer.parseInt(br.readLine());
			oper = new int[4];
			StringTokenizer st = new StringTokenizer(br.readLine());
			for (int i = 0; i < 4; i++) {
				oper[i] = Integer.parseInt(st.nextToken());
				operCnt += oper[i];
			}

			arr = new int[N];
			st = new StringTokenizer(br.readLine());
			for (int i = 0; i < N; i++) {
				arr[i] = Integer.parseInt(st.nextToken());
			}

			recursion(arr[0], oper[0], oper[1], oper[2], oper[3], 0);
			
			answer = maxVal - minVal;
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}

		System.out.println(sb.toString());
	}

	static void recursion(int num, int sum, int sub, int mul, int div, int depth) {
		if (sum < 0 || sub < 0 || mul < 0 || div < 0) {
			return;
		}
		if (depth == operCnt) {
			maxVal = Math.max(maxVal, num);
			minVal = Math.min(minVal, num);
			return;
		}
		recursion(num + arr[depth + 1], sum - 1, sub, mul, div, depth + 1);
		recursion(num - arr[depth + 1], sum, sub - 1, mul, div, depth + 1);
		recursion(num * arr[depth + 1], sum, sub, mul - 1, div, depth + 1);
		recursion(num / arr[depth + 1], sum, sub, mul, div - 1, depth + 1);
	}
}
```

# 23.02.14(화)
* 