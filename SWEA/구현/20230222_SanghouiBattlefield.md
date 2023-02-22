# SWEA 1873 - 상호의 배틀필드
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5LyE7KD2ADFAXc

### 이 문제를 풀기 위한 과정
문제를 천천히 읽고 요구사항대로 구현해주면 된다.

CODE1
```java
import java.util.*;
import java.io.*;

class Solution {
	static int[] dir_x = { -1, 0, 1, 0 };
	static int[] dir_y = { 0, 1, 0, -1 };
	static char[][] map;
	static Tank tank;
	static int H, W;

	public static void main(String args[]) throws Exception {
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for (int test_case = 1; test_case <= T; test_case++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			H = Integer.parseInt(st.nextToken());
			W = Integer.parseInt(st.nextToken());

			map = new char[H][W];

			for (int i = 0; i < H; i++) {
				String input = br.readLine();
				for (int j = 0; j < W; j++) {
					map[i][j] = input.charAt(j);
					if (map[i][j] == '^') {
						tank = new Tank(i, j, 0);
						map[i][j] = '.';
					} else if (map[i][j] == 'v') {
						tank = new Tank(i, j, 2);
						map[i][j] = '.';
					} else if (map[i][j] == '<') {
						tank = new Tank(i, j, 3);
						map[i][j] = '.';
					} else if (map[i][j] == '>') {
						tank = new Tank(i, j, 1);
						map[i][j] = '.';
					}
				}
			}

			int N = Integer.parseInt(br.readLine());

			String s_oper = br.readLine();
			for (int i = 0; i < N; i++) {
				char oper = s_oper.charAt(i);
				runOper(oper);
			}
			
			arriveTank();
			
			sb.append("#").append(test_case).append(" ");
			for (int i = 0; i < H; i++) {
				for (int j = 0; j < W; j++) {
					sb.append(map[i][j]);
				}
				sb.append("\n");
			}
		}

		System.out.println(sb.toString());

	}

	static void arriveTank() {
		if (tank.head == 0) {
			map[tank.x][tank.y] = '^';
		} else if (tank.head == 1) {
			map[tank.x][tank.y] = '>';
		} else if (tank.head == 2) {
			map[tank.x][tank.y] = 'v';
		} else if (tank.head == 3) {
			map[tank.x][tank.y] = '<';
		}
	}

	static void runOper(char oper) {
		switch (oper) {
		case 'U':
			tank.head = 0;
			move(tank.x, tank.y, 0);
			break;
		case 'R':
			tank.head = 1;
			move(tank.x, tank.y, 1);
			break;
		case 'D':
			tank.head = 2;
			move(tank.x, tank.y, 2);
			break;
		case 'L':
			tank.head = 3;
			move(tank.x, tank.y, 3);
			break;
		case 'S':
			shooting();
			break;
		}
	}

	static void shooting() {
		int x = tank.x;
		int y = tank.y;

		if (tank.head == 0) // x가 감소
		{
			while (true) {
				x--;
				if(check(x, y) == false)
					return;
				if (map[x][y] == '*') {
					map[x][y] = '.';
					return;
				} else if (map[x][y] == '#') {
					return;
				}
			}
		} else if (tank.head == 1) // y 가 증가
		{
			while (true) {
				y++;
				if(check(x, y) == false)
					return;
				if (map[x][y] == '*') {
					map[x][y] = '.';
					return;
				} else if (map[x][y] == '#') {
					return;
				}
			}

		} else if (tank.head == 2) // x가 증가
		{
			while (true) {
				x++;
				if(check(x, y) == false)
					return;
				if (map[x][y] == '*') {
					map[x][y] = '.';
					return;
				} else if (map[x][y] == '#') {
					return;
				}
			}

		} else if (tank.head == 3) // y가 감소
		{
			while (true) {
				y--;
				if(check(x, y) == false)
					return;
				if (map[x][y] == '*') {
					map[x][y] = '.';
					return;
				} else if (map[x][y] == '#') {
					return;
				}
			}
		}
	}
	static boolean check(int x, int y)
	{
		if (x < 0 || y < 0 || x >= H || y >= W) {
			return false;
		}
		return true;
	}
	static void move(int x, int y, int dir) {
		int nx = x + dir_x[dir];
		int ny = y + dir_y[dir];
//		if (nx < 0 || ny < 0 || nx >= H || ny >= W) {
//			return;
//		}
		if(check(nx, ny) == false)
			return;

		if (map[nx][ny] == '.') {
			tank.x = nx;
			tank.y = ny;
		}
	}

	static class Tank {
		int x;
		int y;
		int head; // 0, 1, 2, 3 위 오른쪽 아래 왼쪽

		public Tank(int x, int y, int head) {
			this.x = x;
			this.y = y;
			this.head = head;
		}

	}
}
```

# 23.02.13(월)
* 
