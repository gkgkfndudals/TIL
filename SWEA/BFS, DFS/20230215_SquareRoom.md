# SWEA 1861 - 정사각형 방
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5LtJYKDzsDFAXc

### 이 문제를 풀기 위한 과정
이중 for문을 돌면서 BFS를 해주면 풀리는 문제이다.

CODE1
```java
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.util.Queue;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Collections;

class Solution
{
	static int[][] map; 
	static ArrayList<Pair> answer;
	static int N;
	static int[] dir_x = {-1, 0 , 1, 0};
	static int[] dir_y = {0, 1, 0, -1};
	
	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T= Integer.parseInt(br.readLine());

		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = new ArrayList<>();
			N = Integer.parseInt(br.readLine());
			map = new int[N][N];
			
			for(int i = 0; i < N; i++)
			{
				StringTokenizer st = new StringTokenizer(br.readLine());
				for(int j = 0 ; j < N; j++)
				{
					map[i][j] = Integer.parseInt(st.nextToken());
				}
			}
			
			for(int i = 0; i < N; i++)
			{
				for(int j = 0; j < N; j++)
				{
					BFS(i, j, map[i][j]);
				}
			}
			
			Collections.sort(answer);
			
			sb.append("#").append(test_case).append(" ");
			sb.append(answer.get(0).room).append(" ").append(answer.get(0).cnt).append("\n");
		}
		
		System.out.println(sb.toString());
	}
	
	static void BFS(int startX, int startY, int room)
	{
		int count = 1;
		Queue<Room> q = new ArrayDeque<Room>();
		q.offer(new Room(startX, startY, room));
		
		while(!q.isEmpty())
		{
			int x = q.peek().x;
			int y = q.peek().y;
			int currentVal = q.peek().val;
			q.poll();
			
			for(int i = 0; i < 4; i++)
			{
				
				int nx = x + dir_x[i];
				int ny = y + dir_y[i];
				
				if(nx < 0 || ny < 0 || nx >= N || ny >= N || map[nx][ny] != currentVal + 1)
					continue;
				
				count++;
				q.offer(new Room(nx, ny, map[nx][ny]));
			}
		}
		
		answer.add(new Pair(room, count));
	}
	
	static class Pair implements Comparable<Pair>{
		int room;
		int cnt;
		public Pair(int room, int cnt) {
			super();
			this.room = room;
			this.cnt = cnt;
		}
	
		public int compareTo(Pair o)
		{
			if(this.cnt == o.cnt)
			{
				return this.room - o.room;
			}
			return -(this.cnt - o.cnt);
		}
		
		
	}
	static class Room{
		int x;
		int y;
		int val;
		
		public Room(int x, int y, int val) {
			this.x = x;
			this.y = y;
			this.val = val;
		}
	}
}
```

# 23.02.15(수)
* 