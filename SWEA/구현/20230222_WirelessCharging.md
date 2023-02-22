# SWEA 5644 - 무선 충전
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWXRDL1aeugDFAUo

### 이 문제를 풀기 위한 과정
문제를 천천히 읽고 요구사항대로 구현해주면 된다.  
처음에 문제에 예외적인 조건이 많아 엄청 헷갈렸었다.  
그런데, 문제에서 모든 사용자가 충전한 양의 합의 최댓값을 구하라고 하였으므로 그냥 이중 for문을 돌면서 모든 UserA, userB 모든 bc의 경우의 수를 탐색하고 max를 갱신해주면 된다는 걸 깨달았다.

CODE1
```java
import java.util.*;
import java.io.*;

class Solution {
	static ArrayList<Integer> userA;
	static ArrayList<Integer> userB;
	static ArrayList<BC> bc;
	static int M, A;
	static int[] dir_x = { 0, -1, 0, 1, 0 };
	static int[] dir_y = { 0, 0, 1, 0, -1 };

	public static void main(String args[]) throws Exception {
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for (int test_case = 1; test_case <= T; test_case++) {
			userA = new ArrayList<Integer>();
			userB = new ArrayList<Integer>();
			bc = new ArrayList<BC>();

			StringTokenizer st = new StringTokenizer(br.readLine());
			M = Integer.parseInt(st.nextToken()); // 이동시간
			A = Integer.parseInt(st.nextToken()); // BC의 갯수

//			visited = new boolean[2][A];

			st = new StringTokenizer(br.readLine());
			for (int i = 0; i < M; i++) {
				userA.add(Integer.parseInt(st.nextToken()));
			}
			st = new StringTokenizer(br.readLine());
			for (int i = 0; i < M; i++) {
				userB.add(Integer.parseInt(st.nextToken()));
			}

			for (int i = 0; i < A; i++) {
				st = new StringTokenizer(br.readLine());
				int y = Integer.parseInt(st.nextToken());
				int x = Integer.parseInt(st.nextToken());
				int c = Integer.parseInt(st.nextToken());
				int p = Integer.parseInt(st.nextToken());
				bc.add(new BC(x, y, c, p));
			}
			///////////////// 입력 끝

			int answer = solution();

			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}

		System.out.println(sb.toString());
	}

	static int solution() {
		int ans = 0;
		User ua = new User(1, 1);
		User ub = new User(10, 10);

		ans += calDist(ua, ub);

		for (int t = 0; t < M; t++) {
			int dirA = userA.get(t);
			int dirB = userB.get(t);

			ua.x = ua.x + dir_x[dirA];
			ua.y = ua.y + dir_y[dirA];

			ub.x = ub.x + dir_x[dirB];
			ub.y = ub.y + dir_y[dirB];

			ans += calDist(ua, ub);
		}

		return ans;
	}

	static int calDist(User ua, User ub) {
		
		int max = 0;
		//모든 UserA, userB 모든 bc의 경우의 수를 탐색한다.
		for(int i = 0; i < A; i++)
		{
			for(int j = 0; j < A; j++)
			{
				int sum = 0;
				int chargeA = Math.abs(ua.x - bc.get(i).x) + Math.abs(ua.y - bc.get(i).y) <= bc.get(i).c ? bc.get(i).p : 0;
				int chargeB = Math.abs(ub.x - bc.get(j).x) + Math.abs(ub.y - bc.get(j).y) <= bc.get(j).c ? bc.get(j).p : 0;
				
				if(i != j)
					sum = chargeA + chargeB;
				else
					sum = Math.max(chargeA, chargeB);
				
				max = Math.max(max, sum);
			}
		}
		
		return max;
	}

	static class User {
		int x;
		int y;

		public User(int x, int y) {
			this.x = x;
			this.y = y;
		}
	}

	static class BC {
		int x;
		int y;
		int c; // 충전 범위
		int p; // 처리량

		public BC(int x, int y, int c, int p) {
			this.x = x;
			this.y = y;
			this.c = c;
			this.p = p;
		}

	}
}
```

# 23.02.22(수)
* 
