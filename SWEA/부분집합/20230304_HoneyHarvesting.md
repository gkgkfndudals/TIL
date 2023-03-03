# SWEA 2115 - 벌꿀채취
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5V4A46AdIDFAWu

### 이 문제를 풀기 위한 과정
1. 

CODE1
```java

import java.util.ArrayList;
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution
{
	static int N, M, C;
	static int[][] map;
	static boolean[] visited;
	static int answer;
	static int[] worker;
	static int benefitTemp;
	
	public static void main(String args[]) throws Exception
	{
		StringBuilder sb = new StringBuilder();
		BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for(int test_case = 1; test_case <= T; test_case++)
		{
			answer = Integer.MIN_VALUE;
			StringTokenizer st = new StringTokenizer(br.readLine());
			N = Integer.parseInt(st.nextToken());
			M = Integer.parseInt(st.nextToken());
			C = Integer.parseInt(st.nextToken());
			
			map = new int[N][N];
			visited = new boolean[N*N];
			worker = new int[2];
			
			for(int i = 0; i < N; i++)
			{
				st = new StringTokenizer(br.readLine());
				for(int j = 0; j < N; j++)
				{
					map[i][j] = Integer.parseInt(st.nextToken());
				}
			}
			
			combi(0, 0);
			
			sb.append("#").append(test_case).append(" ").append(answer).append("\n");
		}
		
		System.out.println(sb.toString());
	}
	
	static void combi(int depth, int idx)
	{
		if(depth == 2)
		{
			int work1 = worker[0]; // 첫번째 일꾼 첫 스타트 지점
			int work2 = worker[1]; // 두번째 일꾼 첫 스타트 지점
			
			if(isPossible(work1, work2))
			{
				// list1(worker1의) 만들기
				benefitTemp = 0;
				int benefit1 = 0;
				ArrayList<HoneyComb> list1 = new ArrayList<>();
				for(int i = work1; i < M + work1; i++)
				{
					int row = i / N;
					int col = i % N;
					list1.add(new HoneyComb(row, col, map[row][col]));
				}
				subSet(0, 0, list1, new ArrayList<>());
				benefit1 += benefitTemp;
				
				// list2(worker2의) 만들기
				benefitTemp = 0;
				int benefit2 = 0;
				ArrayList<HoneyComb> list2 = new ArrayList<>();
				for(int i = work2; i < M + work2; i++)
				{
					int row = i / N;
					int col = i % N;
					list2.add(new HoneyComb(row, col, map[row][col]));
				}
				subSet(0, 0, list2, new ArrayList<>());
				benefit2 += benefitTemp;
				
				answer = Math.max(answer, benefit1 + benefit2);
			}
			return;
		}
		
		for(int i = idx; i < N*N; i++)
		{
			worker[depth] = i;
			combi(depth + 1, i + M);
		}
		
	}
	
	static void subSet(int depth, int benefit, ArrayList<HoneyComb> list, ArrayList<HoneyComb> tempList)
	{
		if(depth == M)
		{
			if(benefit <= C)
			{
				int profit = 0;
				for(int i = 0; i < tempList.size(); i++)
				{
					profit += (int) Math.pow(tempList.get(i).val, 2);
					
				}
				
				benefitTemp = Math.max(benefitTemp, profit);
			}
			
			return;
		}

		tempList.add(list.get(depth));
		subSet(depth + 1, benefit + list.get(depth).val, list, tempList);
		tempList.remove(tempList.size() - 1);
		
		subSet(depth + 1, benefit, list, tempList);
	}
	
	static boolean isPossible(int work1, int work2) {
		
		int w1 = work1 % N;
		int w2 = work2 % N;
		w1 = w1 + M;
		w2 = w2 + M;
		
		if(w1 > N || w2 > N)
		{
			return false;
		}		
		
		return true;
	}
	
	static class HoneyComb {
		int x;
		int y;
		int val;

		public HoneyComb(int x, int y, int val) {
			this.x = x;
			this.y = y;
			this.val = val;
		}
	}
}

```
  
# 23.03.04(토)
* 