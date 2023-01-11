#  SWEA - 원재의 메모리 복구하기 (1289)

### 이 문제를 풀기 위한 과정
메모리 길이가 최대 50이므로 간단하게 이중 for문으로 풀었다.

CODE1

    import java.util.*;
	import java.io.*;

	public class Solution {

		public static void main(String[] args) throws Exception {
			// TODO Auto-generated method stub
			StringBuilder sb = new StringBuilder();
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			int T = Integer.parseInt(br.readLine());
			
			for(int test_case = 1; test_case <= T; test_case++)
			{
				int ans = 0;
				String memory = br.readLine();
				
				int[] origin = new int[memory.length()];
				int[] init = new int[memory.length()];
				
				for(int i = 0; i < memory.length(); i++)
				{
					origin[i] = Integer.parseInt(memory.substring(i, i+1));
					
					if(origin[i] != init[i])
					{
						for(int j = 0; j < memory.length() - i; j++)
						{
							int idx = i + j;
							init[idx] = origin[i];
						}
						
						ans++;
					}
						
				}
				sb.append("#" + test_case + " " + ans + "\n");
			}
			
			System.out.println(sb.toString());
		}
	}

훨씬 간단하게 코드를 짤 수 있다. 굳이 init 배열을 만들고, 2중 for문으로 init배열을 업데이트 해 줄 필요가 없다.
CODE2

	import java.util.*;
	import java.io.*;
	
	public class Solution {
	
		public static void main(String[] args) throws Exception {
			// TODO Auto-generated method stub
			StringBuilder sb = new StringBuilder();
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			int T = Integer.parseInt(br.readLine());
			
			for(int test_case = 1; test_case <= T; test_case++)
			{
				int ans = 0;
				String memory = br.readLine();
				
				char temp = '0';
				for(int i=0; i<memory.length(); i++) {
					if(memory.charAt(i) != temp) {
						ans++;
						temp = memory.charAt(i);
					}
				}
				sb.append("#" + test_case + " " + ans + "\n");
			}
			
			System.out.println(sb.toString());
		}
	}
        
# 23.01.11(수)
* 