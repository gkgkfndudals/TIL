# 백준 1922 - 네트워크 연결
https://www.acmicpc.net/problem/1922

### 이 문제를 풀기 위한 과정
문제에서 모든 컴퓨터를 연결 하되, 컴퓨터를 연결하는 최소 비용을 구하라고 하였으므로, 이 문제는 크루스칼 알고리즘으로 풀 수 있다.

[https://m.blog.naver.com/ndb796/221230994142](https://m.blog.naver.com/ndb796/221230994142)

나동빈의 크루스칼 알고리즘 설명이다.

CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.StringTokenizer;

public class Main {
	static int N, M;
	static ArrayList<Node> graph;
	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		M = Integer.parseInt(br.readLine());
		
		graph = new ArrayList<Node>();
		
		for(int i = 0; i < M; i++)
		{
			StringTokenizer st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			graph.add(new Node(a, b, c));
		}
		
		
		int answer = solution();
		
		System.out.println(answer);
		
	}
	static int solution() {
		int ans = 0;
		Collections.sort(graph);
		
		int[] parent = new int[N+1];
		
		for(int i = 1; i <= N; i++)
		{
			parent[i] = i;
		}
		
		for(int i = 0 ; i < graph.size(); i++)
		{
			Node node = graph.get(i);
			
			if(find_parent(parent, node.v1) != find_parent(parent, node.v2))
			{
				union_parent(parent, node.v1, node.v2);
				ans += node.val;
			}
		}
		
		return ans;
		
	}
	
	static int find_parent(int[] parent, int x)
	{
		if(parent[x] != x)
		{
			parent[x] = find_parent(parent, parent[x]);
		}
		
		return parent[x];
	}
	
	static void union_parent(int[] parent, int a, int b)
	{
		a = find_parent(parent, a);
		b = find_parent(parent, b);
		
		if(a < b)
		{
			parent[b] = a;
		}
		else {
			parent[a] = b;
		}
	}
	static class Node implements Comparable<Node>{
		int v1;
		int v2;
		int val;
		
		public Node(int v1, int v2, int val) {
			super();
			this.v1 = v1;
			this.v2 = v2;
			this.val = val;
		}

		@Override
		public int compareTo(Node o) {
			// TODO Auto-generated method stub
			return this.val - o .val;
		}
		
		
	}

}


```

# 23.02.10(금)
* 
