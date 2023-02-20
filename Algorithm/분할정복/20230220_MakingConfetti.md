# 백준 2630 - 색종이 만들기
https://www.acmicpc.net/problem/2630

### 이 문제를 풀기 위한 과정
전형적인 분할정복 문제이다. 
1. 2차원 배열 map을 계속 4등분을 한다.
2. 각각의 등분한 작은 map의 시작점(행, 열)을 찾고 재귀를 탄다.
3. 그리고 map의 원소값을 전부 더한 후 
4. sum == size * size 이면 black++ 해주고
5. sum == 0 이면 white++ 해주면서 답을 구한다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static int[][] map;
	static int blueCnt;
	static int whiteCnt;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());

		map = new int[N][N];

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			for (int j = 0; j < N; j++) {
				map[i][j] = Integer.parseInt(st.nextToken());
			}
		}

		solution(0, 0, N);
		
		System.out.println(whiteCnt);
		System.out.println(blueCnt);
	}

	static void solution(int r, int c, int size)
	{	
		int sum = 0;
		for(int i = r; i < r + size; i++)
		{
			for(int j = c; j < c + size; j++)
			{
				sum += map[i][j];
			}
		}
		
		if(sum == size * size)
		{
			blueCnt++;
		} else if(sum == 0){
			whiteCnt++;
		} else {
			solution(r, c, size/2);
			solution(r + size/2, c, size/2);
			solution(r, c + size/2, size/2);
			solution(r + size/2, c + size/2, size/2);
		}
	}
}
```

# 23.02.20(월)
* 
