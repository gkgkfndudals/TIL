# 백준 2023 - 신기한 소수
https://www.acmicpc.net/problem/2023

### 이 문제를 풀기 위한 과정
소수 구하는 방법 총 3가지를 알아두면 좋을 것 같다.  
https://velog.io/@changhee09/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%86%8C%EC%88%98%EC%9D%98-%ED%8C%90%EB%B3%84-%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98-%EC%B2%B4


CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main {
	static int N;
	static int[] head = {2, 3, 5, 7};
	static int[] tail = {1, 3, 7, 9};
	static StringBuilder sb = new StringBuilder();
	
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		
		
		for(int i = 0 ; i < head.length; i++)
		{
			solution(0, head[i]);
		}
		
		System.out.println(sb.toString());
	}
	
	static void solution(int depth, int num)
	{
		if(depth == N - 1)
		{
			if(isPrime(num))
			{
				sb.append(num).append("\n");
			}
			return;
		}
		
		for(int i = 0; i < tail.length; i++)
		{
			if(!isPrime(num*10 + tail[i]))
			{
				continue;
			}
			solution(depth + 1, num * 10 + tail[i]);
		}
	}
	
	static boolean isPrime(int x)
	{
		for(int i = 2; i < Math.sqrt(x); i++)
		{
			if(x % i == 0)
			{
				return false;
			}
		}
		return true;
	}

}

```

# 23.02.10(금)
* 
