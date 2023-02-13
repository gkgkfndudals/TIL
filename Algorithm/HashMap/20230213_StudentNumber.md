# 백준 1235 - 학생 번호
https://www.acmicpc.net/problem/1235

### 이 문제를 풀기 위한 과정
이 문제는 HashMap을 이용하면 간단하게 풀 수 있는 쉬운 문제이다.
1. 문자열을 뒤에서 부터 차례대로 짜르고
2. map에 key값으로 포함되어 있는지 확인하고
3. 새로운 key 값 이면, cnt++를 해준다.
4. 마지막으로 cnt == 학생 수 이면 중복이 되지 않는다는 의미이므로 ans를 return 해준다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static String[] input;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		input = new String[N];

		for (int i = 0; i < N; i++) {
			input[i] = br.readLine();
		}

		int answer = solution();

		System.out.println(answer);

	}

	static int solution() {
		int ans = 0;

		int size = input[0].length();

		for (int i = 0; i < size; i++) {
			HashMap<String, Integer> map = new HashMap<>();
			int cnt = 0;
			for (int j = 0; j < N; j++) {
				String s_sub = input[j].substring(size - i - 1, size);
				if (map.containsKey(s_sub)) {
					break;
				} else {
					map.put(s_sub, 1);
					cnt++;
				}
			}

			if (cnt == N) {
				ans = i + 1;
				break;
			}
		}

		return ans;
	}

}

```

# 23.02.13(월)
* Map을 너무 안쓰다보니 메서드를 다 까먹었다... 공부하도록 하자
