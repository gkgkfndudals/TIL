# SWEA 1233 - 사칙연산 유효성 검사
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV141176AIwCFAYD

### 이 문제를 풀기 위한 과정
이 문제는 재귀로 풀 수 있다.

CODE1
```java
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.BufferedReader;
import java.util.StringTokenizer;
import java.io.InputStreamReader;

class Solution {

	public static void main(String args[]) throws Exception {
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		for (int test_case = 1; test_case <= 10; test_case++) {
			int answer = 0;
			int N = Integer.parseInt(br.readLine());
			String[] tree = new String[N + 1];

			StringTokenizer st;
			for (int i = 0; i < N; i++) {
				st = new StringTokenizer(br.readLine());
				int idx = Integer.parseInt(st.nextToken());
				String val = st.nextToken();
				tree[idx] = val;
			}

			for (int i = 1; i < N + 1; i++) {
				int leftExist = 0;
				int rightExist = 0;

				if (i * 2 <= N) {
					leftExist++;
				}
				if ((i * 2) + 1 <= N) {
					rightExist++;
				}

				if (leftExist == 1 && rightExist == 1) {
					// 수식이여야 한다.
					if (tree[i].equals("-") || tree[i].equals("+") || tree[i].equals("*") || tree[i].equals("/")) {
						answer = 1;
					} else {
						answer = 0;
						break;
					}
				} else if (leftExist == 0 && rightExist == 0) {
					// 숫자여야 한다.
					if (!tree[i].equals("-") && !tree[i].equals("+") && !tree[i].equals("*") && !tree[i].equals("/")) {
						answer = 1;
					} else {
						answer = 0;
						break;
					}
				} else {
					answer = 0;
					break;
				}
			}

			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}

		System.out.println(sb.toString());
	}
}
```

# 23.02.14(화)
* 