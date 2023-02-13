# SWEA 1952 - 수영장
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpFQaAQMDFAUq

### 이 문제를 풀기 위한 과정
이 문제는 백트래킹으로도 풀 수가 있다. DP로도 풀 수 있다고 하는데 나중에 공부하자.

1. LinkedList에 이용하는 달을 추가해주었다.
2. 그리고 각각의 달마다 totalCost과 depth를 업데이트해준다.
3. 3개월 이용권을 등록 할 시 이용하는 달 + 3개월 >= 다음 list 원소의 값 일시, depth++를 해준다.
4. 백트래킹이므로 다시 totalCost, depth의 값을 원상복귀 시켜준다.

CODE1
```java
import java.util.LinkedList;
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution {
	static int answer;
	static int cnt;
	static int[] cost;
	static LinkedList<Pair> list;

	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int T = Integer.parseInt(br.readLine());
		
		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = Integer.MAX_VALUE;
			cnt = 0;
			list = new LinkedList<>();
			
			StringTokenizer st = new StringTokenizer(br.readLine());
			cost = new int[4];
			for(int i = 0; i < 4; i++)
			{
				cost[i] = Integer.parseInt(st.nextToken());
			}
			st = new StringTokenizer(br.readLine());
			for(int i = 1; i <= 12; i++)
			{
				int days = Integer.parseInt(st.nextToken());
				if(days != 0)
				{
					list.add(new Pair(i,  days));
					cnt++;
				}
			}
			
			solution(0, 0);
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		
		System.out.println(sb.toString());
	}

	static void solution(int depth, int totalCost) {
		if (depth >= cnt) {
			answer = Math.min(answer, totalCost);
			return;
		}

		for (int i = 0; i < 4; i++) {
			int tempCost = totalCost;
			int tempDepth = depth;
			if (i == 0) // 1일
			{
				totalCost += (list.get(depth).days * cost[i]);
				depth += 1;
			} else if (i == 1) // 1달
			{
				totalCost += cost[i];
				depth += 1;
			} else if (i == 2) // 3달
			{
				totalCost += cost[i];
				int nextMonth = list.get(depth).month + 3 - 1; // 3개월 할 시 그달 포함해야 되므로 -1
				for(int k = depth; k < list.size(); k++)
				{
					if(nextMonth >= list.get(k).month)
					{
						depth++;
					}	
				}
			} else if (i == 3) {
				totalCost += cost[i];
				depth += 12;
			}
			solution(depth, totalCost);
			totalCost = tempCost;
			depth = tempDepth;
		}
	}

	static class Pair {
		int month;
		int days;

		public Pair(int month, int days) {
			this.month = month;
			this.days = days;
		}
	}
}
```

# 23.02.13(월)
* 
