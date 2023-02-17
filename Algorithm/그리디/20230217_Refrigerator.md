# 백준 1828 - 냉장고
http://www.jungol.co.kr/bbs/board.php?bo_table=pbank&code=1828&sca=3050

### 이 문제를 풀기 위한 과정
그리디의 Activity-selection 활동 선택 문제로 유명한 문제이다.
https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/%EA%B7%B8%EB%A6%AC%EB%94%94/20230217_MeetingRoomAssignment.md
이 문제랑 상당히 비슷하다. 

다른점은 정렬된 list에서 전리스트의 끝 < 다음 리스트 처음 이면, 전 끝값을 다음 리스트 끝값으로 갱신해준다. 
=> p.y < list.get(i).x 이면  p.y = list.get(i).y 으로 갱신해준다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static ArrayList<Pair> list = new ArrayList<>();

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int num1 = Integer.parseInt(st.nextToken());
			int num2 = Integer.parseInt(st.nextToken());

			list.add(new Pair(num1, num2));
		}

		int answer = solution();
		
		System.out.println(answer);
	}

	static int solution() {
		int ans = 1;

		Collections.sort(list);
		
		Pair p = list.get(0);
		for(int i = 1; i < list.size(); i++)
		{
			if(p.y < list.get(i).x)
			{
				p.y = list.get(i).y;
				ans++;
			}
		}

		return ans;
	}

	static class Pair implements Comparable<Pair> {
		int x;
		int y;

		public Pair(int x, int y) {
			this.x = x;
			this.y = y;
		}

		public int compareTo(Pair o) {
			return this.y == o.y ? this.x - o.x : this.y - o.y;
		}
	}
}
```

# 23.02.17(금)
* 
