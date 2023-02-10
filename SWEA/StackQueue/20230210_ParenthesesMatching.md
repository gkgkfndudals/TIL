# SWEA 1218 - 괄호 짝짓기
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14eWb6AAkCFAYD

### 이 문제를 풀기 위한 과정
stack 문제이다.

CODE1
```java
import java.util.Scanner;
import java.util.Stack;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution {
	public static void main(String args[]) throws Exception {
		StringBuilder sb = new StringBuilder();

		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		for (int test_case = 1; test_case <= 10; test_case++) {
			int answer = 1;

			int N = Integer.parseInt(br.readLine());

			String input = br.readLine();

			Stack<Character> stack = new Stack<>();

			for (int i = 0; i < N; i++) {
				char ch = input.charAt(i);
				if (ch == '(' || ch == '{' || ch == '<' || ch == '[') {
					stack.push(input.charAt(i));
				} else {
					char pop = stack.pop();
					if (ch == ')') {
						if (pop != '(') {
							answer = 0;
							break;
						}
					} else if (ch == '}') {
						if (pop != '{') {
							answer = 0;
							break;
						}
					} else if (ch == ']') {
						if (pop != '[') {
							answer = 0;
							break;
						}
					} else if (ch == '>') {
						if (pop != '<') {
							answer = 0;
							break;
						}
					}
				}
			}
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}

		System.out.println(sb.toString());
	}
}

```

# 23.02.10(금)
* 
