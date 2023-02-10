# SWEA 1225 - 암호생성기
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14uWl6AF0CFAYD

### 이 문제를 풀기 위한 과정
이 문제는 Queue로 풀어야 되지만 그냥 배열을 N+1으로 만들어서 풀었다.
배열값을 하나씩 왼쪽으로 땡긴다음 arr[8] = arr[0] - subNum 해주었다.

CODE1
```java
import java.util.Scanner;
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

class Solution
{
	public static void main(String args[]) throws Exception
	{
		
		StringBuilder sb = new StringBuilder();
		BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
		
		for(int test_case = 1; test_case <= 10; test_case++)
		{	
			int t = Integer.parseInt(br.readLine());
			StringTokenizer st = new StringTokenizer(br.readLine());
			
			int[] arr= new int[9];
			
			for(int i = 1; i < arr.length; i++)
			{
				arr[i] = Integer.parseInt(st.nextToken());
			}
			
			int subNum = 1;
			while(arr[8] > 0)
			{
				
				for(int i = 0; i < arr.length - 1; i++)
				{
					arr[i] = arr[i+1];
				}
				arr[8] = arr[0] - subNum;
				
				subNum++;
				
				if(subNum == 6)
				{
					subNum = 1;
				}
				
			}
			arr[8] = 0;
			
			sb.append("#").append(t).append(" ");
			for(int i = 1; i <= 8; i++)
			{
				sb.append(arr[i]).append(" ");
			}
			sb.append("\n");
		}
		
		System.out.println(sb.toString());
	}
}

```

# 23.02.10(금)
* 
