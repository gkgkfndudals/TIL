# 백준 16987 - 계란으로 계란치기
https://www.acmicpc.net/problem/16987

### 이 문제를 풀기 위한 과정
이 문제는 전형적인 백트래킹 문제이다. 못풀어서 답안을 봤다.  

꼭 다시 풀어보자.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static ArrayList<Egg> list;
	static int answer = Integer.MIN_VALUE;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		list = new ArrayList<Egg>();

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			list.add(new Egg(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
		}

		if (N == 1) {
			System.out.println(0);
			return;
		}

		solution(0);

		System.out.println(answer);
	}

	static void solution(int left) {
		if (left >= N) {
			int cnt = 0;
			for (int i = 0; i < N; i++) {
				if (list.get(i).durability <= 0) {
					cnt++;
				}
			}
			answer = Math.max(answer, cnt);
			return;
		}

		Egg fromEgg = list.get(left);

		if (fromEgg.durability <= 0) {
			solution(left + 1);
			return;
		}

		boolean flag = false;
		for (int i = 0; i < N; i++) {
			Egg toEgg = list.get(i);

			if (left == i)
				continue;
			if (toEgg.durability <= 0)
				continue;

			int fromDurability = fromEgg.durability;
			int toDurability = toEgg.durability;
			fromEgg.durability = fromEgg.durability - toEgg.weight;
			toEgg.durability = toEgg.durability - fromEgg.weight;

			flag = true;

			solution(left + 1);

			fromEgg.durability = fromDurability;
			toEgg.durability = toDurability;
		}
		
		if (flag == false) {
			solution(left + 1);
		}

	}

	static class Egg {
		int durability;
		int weight;

		public Egg(int durability, int weight) {
			this.durability = durability;
			this.weight = weight;
		}
	}

}
```

# 23.02.21(화)
* 