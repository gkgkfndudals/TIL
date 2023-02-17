# 백준 1931 - 회의실 배정
https://www.acmicpc.net/problem/1931
  
### 이 문제를 풀기 위한 과정
그리디의 Activity-selection 활동 선택 문제로 유명한 문제이다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static ArrayList<Pair> list;
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		int answer = 0;
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		N = Integer.parseInt(br.readLine());
		list = new ArrayList<>();
		
		for(int i = 0 ; i < N; i++)
		{
			StringTokenizer st = new StringTokenizer(br.readLine());
			int s = Integer.parseInt(st.nextToken());
			int e = Integer.parseInt(st.nextToken());
			list.add(new Pair(s, e));
		}
		
		Collections.sort(list);
		
		Pair p = list.get(0);
		for (int i = 1; i < N; i++) {
			if(p.end <= list.get(i).start)
			{
				p = list.get(i);
				answer++;
			}
		}
		
		System.out.println(answer + 1);
	}
	
	static class Pair implements Comparable<Pair> {
		int start;
		int end;
		public Pair(int start, int end) {
			super();
			this.start = start;
			this.end = end;
		}
		
		public int compareTo(Pair o)
		{
			return this.end != o.end ? this.end - o.end : this.start - o.start;
		}
		
	}

}
```


# 23.02.17(금)
* 
