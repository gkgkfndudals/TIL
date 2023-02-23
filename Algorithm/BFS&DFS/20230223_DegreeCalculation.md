# 백준 2644 - 촌수 계산
https://www.acmicpc.net/problem/2644

### 이 문제를 풀기 위한 과정
CODE3은 트리로 풀려고 했는데 Node root 한개에 계속 연결하여 insert하다보니 또 다른 트리가 나오는 경우가 있어서 풀지 못하였다.

그래서 CODE2 방법이 있다는 것을 알았다. 트리를 배열로 관리 할 수 있다는 게 신기하였다.

하지만 이 문제는 정석으로 풀면 BFS 문제이기 때문에 CODE1 처럼 푸는 게 맞다. (사실 못 풀어서 답안을 봤다....)

**단방향 그래프로 생각하지말고 양방향 그래프로 생각하고 문제를 접근하자.**  
그리고 BFS를 돌리면 답이 구해진다.  


CODE1
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static int start, end;
	static int M;
	static boolean[] visited;
	static ArrayList<Integer>[] graph;
	static int answer = -1;
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());
		visited = new boolean[N+1];
		
		graph = new ArrayList[N+1];
		for(int i = 0; i < N+ 1; i++)
		{
			graph[i] = new ArrayList<Integer>();
		}
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		start = Integer.parseInt(st.nextToken());
		end = Integer.parseInt(st.nextToken());

		M = Integer.parseInt(br.readLine());

		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int p = Integer.parseInt(st.nextToken());
			int c = Integer.parseInt(st.nextToken());
			graph[p].add(c);
			graph[c].add(p);
		}
		
		BFS();

		System.out.println(answer);
	}
	
	static void BFS() {
		
		int depth = 0;
		Queue<Integer> q = new ArrayDeque<>();
		q.offer(start);
		visited[start] = true;

		while(!q.isEmpty())
		{
			int size = q.size();
			
			for(int k = 0; k < size; k++)
			{
				int cur = q.poll();
				
				if(cur == end)
				{
					answer = depth;
					return;
				}
				for(int i = 0; i < graph[cur].size(); i++)
				{
					int next = graph[cur].get(i);
					
					if(visited[next] == true)
						continue;
					
					visited[next] = true;
					q.offer(next);
				}
				
			}
			
			depth++;
		}
		
	}
}
```
  
CODE2
```java
import java.util.*;
public class Main {

	public static int n, m, c1, c2;
	public static Node[] arr;
	public static boolean[] visited;
	public static int[] chonsu;
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		n = sc.nextInt();
		c1 = sc.nextInt(); c2 = sc.nextInt();
		m = sc.nextInt();
		int x, y;
		arr = new Node[n+1];	//0번은 dummy
		visited = new boolean[n+1];
		chonsu = new int[n+1];
		for(int i=0; i<n+1; i++) {
			arr[i] = new Node(i);
			chonsu[i] = -1;
		}
		for(int i=0; i<m; i++) {
			x=sc.nextInt(); y=sc.nextInt();	//y의 부모는 x이다
			arr[y].parent=x;
			arr[x].children.add(y);
		}
		//입력끝
		Queue<Integer>q = new ArrayDeque<>();
		q.offer(c1);
		visited[c1]=true;
		chonsu[c1]=0;
		while(q.isEmpty()==false) {
			int cur = q.poll();
			//부모
			if(!visited[arr[cur].parent]) {
				visited[arr[cur].parent] = true;
				chonsu[arr[cur].parent] = chonsu[cur]+1;
				q.offer(arr[cur].parent);
			}
			//자식
			for(int chi: arr[cur].children) {
				if(visited[chi])continue;
				visited[chi] = true;
				chonsu[chi] = chonsu[cur]+1;
				q.offer(chi);
			}
		}
		System.out.println(chonsu[c2]);
	}
}
class Node{
	public int parent;
	public int num; //인덱스 그대로라 없어도 되는 필드인듯...
	ArrayList<Integer> children;
	Node(int x){
		this.num=x;
		this.parent = 0; //초기값
		this.children = new ArrayList<>();
	}
}
```
  
CODE3
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Main {
	static int N;
	static int p1, p2;
	static int M;
	static Node root = null;

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		N = Integer.parseInt(br.readLine());

		StringTokenizer st = new StringTokenizer(br.readLine());
		p1 = Integer.parseInt(st.nextToken());
		p2 = Integer.parseInt(st.nextToken());

		M = Integer.parseInt(br.readLine());

		st = new StringTokenizer(br.readLine());
		int p = Integer.parseInt(st.nextToken());
		int c = Integer.parseInt(st.nextToken());

		root = new Node(p, 0, null);
		insertNode(root, p, c);
		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			p = Integer.parseInt(st.nextToken());
			c = Integer.parseInt(st.nextToken());
			insertNode(root, p, c);
		}

	}

	static void insertNode(Node root, int p, int c) {
		if (root.num == p) {
			root.child.add(new Node(c, root.degree + 1, root));
		} else {
			for (int i = 0; i < root.child.size(); i++) {
				insertNode(root.child.get(i), p, c);
			}
		}
	}

	static class Node {
		int num;
		int degree;
		Node parent;
		ArrayList<Node> child = new ArrayList<>();

		public Node(int num, int degree, Node parent) {
			this.num = num;
			this.degree = degree;
			this.parent = parent;
		}
	}
}
```


# 23.02.16(목)
* 