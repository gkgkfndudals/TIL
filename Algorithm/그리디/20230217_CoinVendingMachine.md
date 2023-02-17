# 정보올림피아드 1183 - 동전 자판기(下)
http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&code=1183&sca=3050
  
### 이 문제를 풀기 위한 과정
그리디의 문제로써 역발상하는 유명한 유형의 문제이다.
https://github.com/gkgkfndudals/TIL/blob/master/Study/Algo/20230217.md  
마지막 내용에 동전 자판기를 보자.  

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
	static int W;
	static int[] arr = { 500, 100, 50, 10, 5, 1 };
	static int[] money = new int[6];
	static int count;
	static int[] answer = new int[6];

	public static void main(String[] args) throws Exception {
		StringBuilder sb = new StringBuilder();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		W = Integer.parseInt(br.readLine());
		StringTokenizer st = new StringTokenizer(br.readLine());
		int totalMoney = 0;
		for (int i = 0; i < 6; i++) {
			money[i] = Integer.parseInt(st.nextToken());
			totalMoney += money[i] * arr[i];
			count += money[i];
		}
		totalMoney -= W;
		
		
		for(int i = 0; i < 6; i++)
		{
			if(totalMoney >= arr[i])
			{
				int cnt = totalMoney/arr[i];
				if(cnt <= money[i])
				{
					totalMoney = totalMoney - cnt*arr[i];
					money[i] = money[i] - cnt;
					count = count - cnt;
				} else
				{
					totalMoney = totalMoney - money[i]*arr[i];
					count = count - money[i];
					money[i] = 0;
				}
			}
			
		}
		
		sb.append(count).append("\n");
		for(int i = 0; i < 6; i++)
		{
			sb.append(money[i]).append(" ");
		}
		
		System.out.println(sb.toString());
	}

}

```


# 23.02.17(금)
* 
