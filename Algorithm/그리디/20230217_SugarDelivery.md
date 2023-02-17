# 백준 1183 - 설탕 배달
https://www.acmicpc.net/problem/2839

### 이 문제를 풀기 위한 과정
그리디 문제이다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main {
	static int N;
	static int cnt1, cnt2;
	static int answer;
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		
		int n1 = N/ 5;
		
		for(int i = n1; i >= 0; i--)
		{
			int sub = N - i*5;
			
			if(sub % 3 == 0)
			{
				N = sub;
				cnt1 = i;
				break;
			}
		}
		
		if(N % 3 == 0)
		{
			cnt2 = N / 3;			
		}
		
		answer = cnt1 + cnt2;
		
		answer = answer == 0 ? -1 : answer;
		System.out.println(answer);
	}

}
```

# 23.02.17(금)
* 
