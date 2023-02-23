# 백준 1774 - 우주신과의 교감
https://www.acmicpc.net/problem/1774

### 이 문제를 풀기 위한 과정
전형적인 최소 신장 문제이다. 
1. 문제에서 미리 M크기 만큼 연결되어진 Edge가 있다고 하였으므로 입력과 동시에 union해준다.
2. 그리고 모든 정점들간에 Edge를 구하여 edge 리스트에 추가해준다.
3. 그리고 크루스칼 알고리즘을 구현해주면 된다.  

CODE1
```java
import java.io.*;
import java.util.*;

public class Main {
	static int N, M;
	static ArrayList<God> god = new ArrayList<>();
	static ArrayList<Edge> edge = new ArrayList<>();
	static int[] parent;

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());

		parent = new int[N + 1];
		for (int i = 0; i < N + 1; i++) {
			parent[i] = i;
		}

		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine());
			int x = Integer.parseInt(st.nextToken());
			int y = Integer.parseInt(st.nextToken());
			god.add(new God(i + 1, x, y));
		}

		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int n1 = Integer.parseInt(st.nextToken());
			int n2 = Integer.parseInt(st.nextToken());

			God v1 = god.get(n1 - 1);
			God v2 = god.get(n2 - 1);

			double cost = calDist(v1.x, v1.y, v2.x, v2.y);

			union_parent(parent, v1.num, v2.num);
		}

		double answer = solution();
		
		System.out.printf("%.2f", answer);
	}

	static double solution() {
		double ans = 0.0;

		makeEdge();
		
		Collections.sort(edge);
		
		for(int i = 0; i < edge.size(); i++)
		{
			God v1 = edge.get(i).v1;
			God v2 = edge.get(i).v2;
			if(find_parent(parent, v1.num) != find_parent(parent, v2.num))
			{
				union_parent(parent, v1.num, v2.num);
				ans += edge.get(i).cost;
			}
		}
		
		return ans;
	}

	static void makeEdge() {
		for (int i = 0; i < N; i++) {
			God v1 = god.get(i);
			for (int j = i + 1; j < N; j++) {
				God v2 = god.get(j);
				double cost = calDist(v1.x, v1.y, v2.x, v2.y);

				edge.add(new Edge(v1, v2, cost));
			}
		}
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

	static double calDist(int x1, int y1, int x2, int y2) {
		return Math.sqrt(Math.pow(x1 - x2, 2) + Math.pow(y1 - y2, 2));
	}

	static class Edge implements Comparable<Edge> {
		God v1;
		God v2;
		double cost;

		public Edge(Main.God v1, Main.God v2, double cost) {
			this.v1 = v1;
			this.v2 = v2;
			this.cost = cost;
		}

		public int compareTo(Edge o) {
			return (int) ((this.cost - o.cost) * 100);
		}
	}

	static class God {
		int num;
		int x;
		int y;

		public God(int num, int x, int y) {
			this.num = num;
			this.x = x;
			this.y = y;
		}
	}
}
```

# 23.02.23(목)
* 