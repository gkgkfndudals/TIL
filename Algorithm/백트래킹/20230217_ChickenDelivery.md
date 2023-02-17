# 백준 15686 - 치킨 배달
https://www.acmicpc.net/problem/15686

### 이 문제를 풀기 위한 과정
백트래킹 문제이다. 백준의 연구소 문제랑 상당히 비슷하다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.ArrayList;

public class Main {
	static int N , M;
	static int[][] map;
	static ArrayList<Pair> chicken = new ArrayList<>();
	static ArrayList<Pair> house = new ArrayList<>();
	static Pair[] p;
	static int answer = Integer.MAX_VALUE;
	
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		map = new int[N][N];
		p = new Pair[M];
		
		for(int i = 0; i < N; i++)
		{
			st = new StringTokenizer(br.readLine());
			for(int j = 0; j < N; j++)
			{
				map[i][j] = Integer.parseInt(st.nextToken());
				if(map[i][j] == 2)
				{
					chicken.add(new Pair(i, j));
				}
				else if(map[i][j] == 1)
				{
					house.add(new Pair(i, j));
				}
			}
		}
		
		combination(0, 0);
		
		System.out.println(answer);
	}
	
	static void combination(int depth, int idx)
	{
		if(depth == M)
		{
			int totalDist = 0;
			for(int i = 0; i < house.size(); i++)
			{
				int dist = Integer.MAX_VALUE;
				Pair h = house.get(i);
				for(int j = 0; j < M; j++)
				{
					Pair c = p[j];
					int val = Math.abs(c.x - h.x) + Math.abs(c.y - h.y);
					dist = val < dist ? val : dist;
//					dist = Math.min(val, dist);
				}
				
				totalDist += dist;
				
			}
			
			answer = totalDist < answer ? totalDist : answer;
//			answer = Math.min(totalDist, answer);
			
			
			return;
		}
		
		for(int i = idx; i < chicken.size(); i++)
		{
			p[depth] = chicken.get(i);
			combination(depth + 1, i + 1);
		}
	}
	
	static class Pair {
		int x;
		int y;
		
		public Pair(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}
	

}
```

# 23.02.17(금)
* 
