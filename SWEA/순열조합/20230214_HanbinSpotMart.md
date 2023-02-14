# SWEA 9229 - 한빈이와 Spot Mart
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AW8Wj7cqbY0DFAXN

### 이 문제를 풀기 위한 과정
이 문제는 N이 최대 1000이므로 부분집합으로 풀면 O(2^1000)으로 시간초과가 나온다.  
문제에서 과자는 무조건 2봉지만 사야된다고 명시를 해놨으므로 nC2만을 구하면 된다.
결과적으로 O(N^2) 으로 풀 수 있다. nCr -> O(N^R)

CODE1
```java
import java.util.Scanner;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.ArrayList;

class Solution
{
	static int N, M;
	static int[] arr;
	static int answer;
	static int[] brr;
	
	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());
	
		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = -1;
			StringTokenizer st = new StringTokenizer(br.readLine());
			N = Integer.parseInt(st.nextToken());
			M = Integer.parseInt(st.nextToken());
			
			arr = new int[N];
			
			brr = new int[N];
			
			st = new StringTokenizer(br.readLine());
			for(int i = 0; i < N; i++)
			{
				arr[i] = Integer.parseInt(st.nextToken());
			}
			
			combination(0, 0, 0);
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		
		System.out.println(sb.toString());
	}
	
	static void combination(int depth, int idx, int weights)
	{
		if(depth == 2)
		{
			if(weights <= M)
			{
				answer = Math.max(answer, weights);				
			}
			return;
		}
		
		for(int i = idx; i < arr.length; i++)
		{
			combination(depth + 1, i + 1, weights + arr[i] );
		}
		
	}
}
```

# 23.02.14(화)
* 