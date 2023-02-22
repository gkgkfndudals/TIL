# SWEA 1247 - 최적 경로
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV15OZ4qAPICFAYD

### 이 문제를 풀기 위한 과정
처음에는 문제 제목이 최적경로 이여서 다익스트라 인줄 알았는데 읽어보니 순열, 백트래킹 문제였다.

CODE1
```java
import java.util.*;
import java.io.*;

class Solution
{
	static int answer;
	static int N;
	static Pair company;
	static Pair house;
	static ArrayList<Pair> list;
	static boolean[] visited;
	
	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());
		
		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = Integer.MAX_VALUE;
			N = Integer.parseInt(br.readLine());
			visited = new boolean[N];
			
			StringTokenizer st = new StringTokenizer(br.readLine());
			
			company = new Pair(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
			house = new Pair(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken()));
			
			list = new ArrayList<>();
			for(int i = 0; i < N; i++)
			{
				list.add(new Pair(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
			}
			
			solution(0, company, 0);
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		
		System.out.println(sb.toString());
	}
	
	static void solution(int depth, Pair start, int dist)
	{
		if(depth == N)
		{
			// 고객들 모두 방문하고 집으로 가는 거리
			int absX = Math.abs(start.x - house.x);
			int absY = Math.abs(start.y - house.y);
			dist = dist + absX + absY;
			
			answer = Math.min(answer, dist);
			return;
		}
		
		for(int i = 0; i < N; i++)
		{
			// 시작점과 끝점의 거리 계산
			if(visited[i] == true)
				continue;

			int absX = Math.abs(start.x - list.get(i).x);
			int absY = Math.abs(start.y - list.get(i).y);
			int temp = dist;
			dist = dist + absX + absY;
			visited[i] = true;
			solution(depth + 1, list.get(i), dist);
			dist = temp;
			visited[i] = false;
		}
	}
	
	static class Pair{
		int x;
		int y;
		
		public Pair(int x, int y) {
			this.x = x;
			this.y = y;
		}		
	}
}
```

# 23.02.13(월)
* 
