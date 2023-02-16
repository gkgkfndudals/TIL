# 백준 4386 - 별자리 만들기
https://www.acmicpc.net/problem/4386

### 이 문제를 풀기 위한 과정
크루스칼 알고리즘으로 풀면 된다. 문제에서 정수의 값으로 입력, 출력해야 되는 부분이 너무 귀찮았다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;

public class Main {
	static int N;
	static Vortex[] vortex;
	static ArrayList<Edge> edge;
	static int[] arr;

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		double answer = 0.0;
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		vortex = new Vortex[N];

		for (int i = 0; i < N; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			double x = Double.parseDouble(st.nextToken());
			double y = Double.parseDouble(st.nextToken());
			vortex[i] = new Vortex(i + 1, x, y);
		}
		edge = new ArrayList<>();

		arr = new int[2];
		combination(0, 0);
		answer = solution();
	
		System.out.printf("%.2f", answer);
	}

	static double solution() {
		double ans = 0.0;
		int[] parent = new int[N + 1];

		for (int i = 0; i < N + 1; i++) {
			parent[i] = i;
		}

		Collections.sort(edge);

		for (int i = 0; i < edge.size(); i++) {
			Edge e = edge.get(i);
			if (find_parent(parent, e.v1.num) != find_parent(parent, e.v2.num)) {
				union_parent(parent, e.v1.num, e.v2.num);
				ans += e.cost;
			}
		}

		return ans;

	}

	static int find_parent(int[] parent, int x) {
		if (parent[x] != x) {
			parent[x] = find_parent(parent, parent[x]);
		}
		return parent[x];
	}

	static void union_parent(int[] parent, int a, int b) {
		a = find_parent(parent, a);
		b = find_parent(parent, b);

		if (a < b) {
			parent[b] = a;
		} else {
			parent[a] = b;
		}
	}

	static void combination(int depth, int idx) {
		if (depth == 2) {
			int v1 = arr[0];
			int v2 = arr[1];

			double dist = findDist(vortex[v1], vortex[v2]);

			edge.add(new Edge(vortex[v1], vortex[v2], dist));

			return;
		}

		for (int i = idx; i < N; i++) {
			arr[depth] = i;
			combination(depth + 1, i + 1);
		}
	}

	static double findDist(Vortex v1, Vortex v2) {
		double absX = Math.abs(v2.x - v1.x);
		double absY = Math.abs(v2.y - v1.y);

		return Math.sqrt(Math.pow(absX, 2) + Math.pow(absY, 2));
	}

	static class Vortex {
		int num;
		double x;
		double y;

		public Vortex(int num, double x, double y) {
			this.num = num;
			this.x = x;
			this.y = y;
		}

	}

	static class Edge implements Comparable<Edge> {
		Vortex v1;
		Vortex v2;
		double cost;

		public Edge(Vortex v1, Vortex v2, double cost) {
			super();
			this.v1 = v1;
			this.v2 = v2;
			this.cost = cost;
		}

		public int compareTo(Edge o) {
			return (int) ((this.cost - o.cost) * 100);
		}
	}
}
```

# 23.02.16(목)
* 