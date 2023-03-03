# 백준 16236 - 아기 상어
https://www.acmicpc.net/problem/16236

### 이 문제를 풀기 위한 과정
1. 

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Collections;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static int[][] map;
	static Shark shark;
	static ArrayList<Fish> list[];
	static int[] dir_x = { -1, 0, 1, 0 };
	static int[] dir_y = { 0, 1, 0, -1 };
	static int answer;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		map = new int[N][N];
		list = new ArrayList[7];
		for (int i = 0; i < 7; i++) {
			list[i] = new ArrayList<Fish>();
		}

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
				if (map[i][j] == 9) {
					shark = new Shark(i, j, 2, 0);
				} else {
					if (map[i][j] != 0) {
						list[map[i][j]].add(new Fish(i, j, map[i][j], 0));
					}
				}
			}
		}

		while(true)
		{
			if(calDist() == false)
				break;
		}

		System.out.println(answer);
	}

	static void BFS(Fish fish) {
		boolean[][] visited = new boolean[N][N];

		Queue<Pair> q = new ArrayDeque<>();

		q.offer(new Pair(shark.x, shark.y));
		visited[shark.x][shark.y] = true;
		int dist = 0;

		while (!q.isEmpty()) {
			dist++;
			int size = q.size();

			for (int i = 0; i < size; i++) {
				Pair p = q.poll();

				for (int d = 0; d < 4; d++) {
					int nx = p.x + dir_x[d];
					int ny = p.y + dir_y[d];

					if (nx < 0 || ny < 0 || nx >= N || ny >= N || visited[nx][ny] == true)
						continue;

					if (shark.size < map[nx][ny])
						continue;

					visited[nx][ny] = true;
					q.offer(new Pair(nx, ny));

					if (fish.x == nx && fish.y == ny) {
						fish.dist = dist;
						return;
					}
				}
			}

		}
	}

	static boolean calDist() {
		PriorityQueue<Fish> pq = new PriorityQueue<Fish>();
		
//		System.out.println(shark.toString());
//		for (int i = shark.size - 1; i >= 1; i--) {
		for (int i = 6; i >= 1; i--) {
			if(i >= shark.size)
				continue;
			
			for (int j = 0; j < list[i].size(); j++) {
				
				Fish fish = new Fish(); 
				
				fish.x = list[i].get(j).x;
				fish.y = list[i].get(j).y;
				fish.size = list[i].get(j).size;
				fish.dist = list[i].get(j).dist;
				
				BFS(fish);
				
//				System.out.println(fish.toString());
				if(fish.dist != 0)
				{
					pq.offer(fish);
					
				}
			}
		}
//		System.out.println();
		
		if (pq.isEmpty())
			return false;

		Fish f = pq.poll();
		for (int i = 0; i < list[f.size].size(); i++) {
			if (list[f.size].get(i).x == f.x && list[f.size].get(i).y == f.y)
			{
				list[f.size].remove(i);
				map[f.x][f.y] = 0;
			}
		}

		map[shark.x][shark.y] = 0;
		shark.x = f.x;
		shark.y = f.y;
		shark.exp++;
		if (shark.exp == shark.size) {
			shark.size++;
			shark.exp = 0;
		}
		answer += f.dist;

		pq.clear();
		
		return true;
	}

	static class Shark {
		int x;
		int y;
		int size;
		int exp;

		public Shark(int x, int y, int size, int exp) {
			this.x = x;
			this.y = y;
			this.size = size;
			this.exp = exp;
		}

		@Override
		public String toString() {
			return "Shark [x=" + x + ", y=" + y + ", size=" + size + ", exp=" + exp + "]";
		}

		
	}

	static class Fish implements Comparable<Fish> {
		int x;
		int y;
		int size;
		int dist;

		
		public Fish() {
			
		}

		public Fish(int x, int y, int size) {
			this.x = x;
			this.y = y;
			this.size = size;
		}

		public Fish(int x, int y, int size, int dist) {
			this.x = x;
			this.y = y;
			this.size = size;
			this.dist = dist;
		}

		public int compareTo(Fish o) {
			if (this.dist != o.dist) {
				return this.dist - o.dist;
			} else if (this.x != o.x) {
				return this.x - o.x;
			} else {
				return this.y - o.y;
			}
		}

		@Override
		public String toString() {
			return "Fish [x=" + x + ", y=" + y + ", size=" + size + ", dist=" + dist + "]";
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
  
# 23.03.03(금)
* 