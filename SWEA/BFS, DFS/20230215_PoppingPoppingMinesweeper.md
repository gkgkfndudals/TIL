# SWEA 1868 - 파핑파핑 지뢰찾기
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5LwsHaD1MDFAXc

### 이 문제를 풀기 위한 과정
1. 정수 2차원 배열에 지뢰 '*'는 100으로 값을 넣고, 길 '.'은 10으로 값을 넣어 준다.
2. 그리고 이중 for문을 돌면서 각각의 원소의 지뢰 갯수를 구해준다. map[i][j] = cntMine(i, j);
3. 그리고 지뢰가 0인 원소는 BFS를 돌려야 하므로 BFS 함수에 넣어서 순회해준다.
4. 0이 아닌 원소들은 각각 한번씩 무조건 8방위 탐색을 해줘야하므로 visited == false 인 갯수 만큼 정답을 더해준다.

CODE1
```java

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.Queue;

class Solution {
	static int N;
	static int[][] map;
	static int[] dir_x = { -1, -1, -1, 0, 1, 1, 1, 0 };
	static int[] dir_y = { -1, 0, 1, 1, 1, 0, -1, -1 };
	static boolean[][] visited;
	static Queue<Pair> q_zero;
	static Queue<Pair> q;
	static int answer;

	public static void main(String args[]) throws Exception {
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for (int test_case = 1; test_case <= T; test_case++) {
			answer = 0;
			N = Integer.parseInt(br.readLine());
			map = new int[N][N];
			visited = new boolean[N][N];

			q_zero = new ArrayDeque<>();
			q = new ArrayDeque<>();

			for (int i = 0; i < N; i++) {
				String input = br.readLine();
				for (int j = 0; j < N; j++) {
					char c = input.charAt(j);
					if ('.' == c) {
						map[i][j] = 10; // 그냥 길은 10이라고 하겠다.
					} else if ('*' == c) {
						map[i][j] = 100; // 그냥 지뢰는 100으로 하겠다.
						visited[i][j] = true;
					}
				}
			}

			for (int i = 0; i < N; i++) {
				for (int j = 0; j < N; j++) {
					if(map[i][j] != 100) {
						map[i][j] = cntMine(i, j);
						if(map[i][j] == 0)
						{
							q_zero.offer(new Pair(i, j));
						}
					}
				}
			}
			
			
 			while (!q_zero.isEmpty()) {
				Pair p = q_zero.poll();
				BFS(p.x, p.y);
			}
 			
 			for(int i = 0; i < N; i++)
 			{
 				for(int j = 0; j < N; j++)
 				{
 					if(visited[i][j] == false)
 					{
 						answer++;
 					}
 				}
 			}
 			
			
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		System.out.println(sb.toString());
	}

	static void BFS(int startX, int startY) {
		Queue<Pair> q = new ArrayDeque<>();

		if (visited[startX][startY] == true)
			return;

		answer++;
		visited[startX][startY] = true;

		q.offer(new Pair(startX, startY));

		while (!q.isEmpty()) {
			int x = q.peek().x;
			int y = q.peek().y;
			q.poll();
			
			for (int i = 0; i < 8; i++) {
				int nx = x + dir_x[i];
				int ny = y + dir_y[i];

				if (nx < 0 || ny < 0 || nx >= N || ny >= N || map[nx][ny] == 100 || visited[nx][ny] == true)
					continue;
				
				if(map[x][y] == 0)
				{
					q.offer(new Pair(nx, ny));
					visited[nx][ny] = true;
				}
			}
		}

	}

	// 8방위 전부 지뢰가 갯수
	static int cntMine(int x, int y) {
		int cnt = 0;
		for (int d = 0; d < 8; d++) {
			int nx = dir_x[d] + x;
			int ny = dir_y[d] + y;

			if (nx < 0 || ny < 0 || nx >= N || ny >= N) {
				continue;
			}

			if (map[nx][ny] == 100) {
				cnt++;
			}
		}

		return cnt;
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

# 23.02.15(수)
* 처음에 BFS를 한번만 돌면서 전부 처리하려고 하였지만, 하지 못하였다.
* 그래서 cntMine으로 배열의 값을 지뢰의 갯수로 바꿔주고, BFS를 돌렸다.
* 이렇게 하면 for문이 여러번 돌아서 비효율적 일 것 같은데 개선점을 찾아봐야 겠다.