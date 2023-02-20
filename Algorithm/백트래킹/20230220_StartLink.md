# 백준 14889 - 스타트와 링크
https://www.acmicpc.net/problem/14889

### 이 문제를 풀기 위한 과정
이 문제는 전형적인 백트래킹 문제이다. 
1. 문제에서 “이제 N/2명으로 이루어진 스타트 팀과 링크 팀으로 사람들을 나눠야 한다.” 이게 핵심 키워드다. 
2. 기저조건으로 depth == N/2을 해주고, Visited가 true이면 스타트팀, false 이면 링크팀의 능력치 합을 구하여 준다.  
3. 마지막으로 스타트와 링크팀의 능력치 차의 절대값이 최소인 것을 구하여 주면 된다.

이 문제랑 비슷한거 같다.  
https://github.com/gkgkfndudals/TIL/blob/master/SWEA/%EC%88%9C%EC%97%B4%EC%A1%B0%ED%95%A9/20230216_Chef.md


CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static int[][] map;
	static int answer = Integer.MAX_VALUE;
	static boolean[] visited;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		map = new int[N][N];
		visited = new boolean[N];

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
			}
		}

		solution(0, 0);

		System.out.println(answer);

	}

	static void solution(int depth, int idx) {
		if (depth == N / 2) {
			int startTeam = 0;
			int linkTeam = 0;
			
			for(int i = 0; i < N; i++)
			{
				for(int j = i + 1; j < N; j++)
				{
					if(visited[i] == true && visited[j] == true)
					{
						startTeam += map[i][j];
						startTeam += map[j][i];
					}
					else if(visited[i] == false && visited[j] == false)
					{
						linkTeam += map[i][j];
						linkTeam += map[j][i];
					}
				}
			}
			
			
			answer = Math.min(answer, Math.abs(startTeam - linkTeam));
			return;
		}

		for (int i = idx; i < N; i++) {
			if (visited[i])
				continue;

			visited[i] = true;
			solution(depth + 1, i + 1);
			visited[i] = false;
		}
	}
}
```

# 23.02.20(월)
* 