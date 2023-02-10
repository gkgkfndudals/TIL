# SWEA 5215 - 햄버거 다이어트
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWT-lPB6dHUDFAVT

### 이 문제를 풀기 위한 과정
0-1 가방 문제인데 N이 최대 20이여서 부분집합(O(N^20))으로 풀었다. 

CODE1
```java
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution
{
	static int answer;
	static int N, L;
	static Pair[] arr;
	
	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int T = Integer.parseInt(br.readLine());
		
		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = 0;
			StringTokenizer st = new StringTokenizer(br.readLine());
			N = Integer.parseInt(st.nextToken());
			L = Integer.parseInt(st.nextToken());
			
			arr = new Pair[N];
			
			for(int i = 0; i < N; i++)
			{
				st = new StringTokenizer(br.readLine());
				int t = Integer.parseInt(st.nextToken());
				int k = Integer.parseInt(st.nextToken());
				arr[i] = new Pair(t, k); 
			}
			
			subSet(0, 0, 0);
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		
		System.out.println(sb.toString());
	}
	
	static void subSet(int depth, int score, int kalory)
	{
		if(depth == N)
		{

			if(kalory <= L)
			{
				answer = Math.max(answer, score);
			}
			return;
		}
		
		subSet(depth + 1, score + arr[depth].t, kalory + arr[depth].k);
		subSet(depth + 1, score, kalory);
	}
	
	static class Pair {
		int t;
		int k;
		
		public Pair(int t, int k) {
			this.t = t;
			this.k = k;
		}
	}
}

```

# 23.02.10(금)
* 
