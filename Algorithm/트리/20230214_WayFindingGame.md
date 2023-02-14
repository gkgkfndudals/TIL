# 프로그래머스 2019 KAKAO BLIND RECRUITMENT - 길 찾기 게임
https://school.programmers.co.kr/learn/courses/30/lessons/42892

### 이 문제를 풀기 위한 과정
이 문제는 이진트리를 만들어서 전위, 후위를 구하는 문제이다.

CODE1
```java
import java.util.*;

class Solution {
    static int[][] answer;
    static int idx;
    
    public int[][] solution(int[][] nodeinfo) {
        // int[][] answer = {};
        answer = new int[2][nodeinfo.length]; // [전위, 후위][노드 값] 
        Node[] node = new Node[nodeinfo.length];
        
        for(int i = 0; i < node.length; i++)
        {
            node[i] = new Node(nodeinfo[i][0], nodeinfo[i][1], i + 1, null, null);
        }
        
        Arrays.sort(node);
        
        // for(Node n : node)
        // {
        //     System.out.println(n.toString());
        // }
        
        Node root = node[0]; // 현재 node[0]이 y 값이 제일 크므로
        for(int i = 1; i < node.length; i++) // 트리 생성
        {
            insertNode(root, node[i]);
        }
        
        // 전위
        idx = 0;
        preOrder(root);
        // for(int i = 0; i < answer[0].length; i++)
        // {
        //     System.out.print(answer[0][i] + " ");
        // }
        // System.out.println();
        
        // 후위
        idx = 0;
        postOrder(root);
        // for(int i = 0; i < answer[1].length; i++)
        // {
        //     System.out.print(answer[1][i] + " ");
        // }
        
        return answer;
    }
    
    public void postOrder(Node root)
    {
        if(root != null)
        {
            postOrder(root.left);
            postOrder(root.right);
            answer[1][idx++] = root.val;
        }
    }
    
    public void preOrder(Node root)
    {
        if(root != null)
        {
            answer[0][idx++] = root.val;
            preOrder(root.left);
            preOrder(root.right);
        }
    }
    
    public void insertNode(Node parent, Node child)
    {
        // 임의의 노드 V의 왼쪽 서브 트리(left subtree)에 있는 모든 노드의 x값은 V의 x값보다 작다.
        if(parent.x > child.x) 
        {
            if(parent.left == null)
                parent.left = child;
            else
                insertNode(parent.left, child);
        } 
        else {
            if(parent.right == null)
                parent.right = child;
            else
                insertNode(parent.right, child);
        }
    }
    
    public class Node implements Comparable<Node> {
        int x;
        int y;
        int val;
        Node left;
        Node right;
        
        public Node(int x, int y, int val, Node left, Node right)
        {
            this.x = x;
            this.y = y;
            this.val = val;
            this.left = left;
            this.right = right;
        }
        
        public int compareTo(Node o)
        {
            if(this.y == o.y)
                return this.x - o.x; // 그냥 해줌
            else
                return -(this.y - o.y); // 자식 노드의 y 값은 항상 부모 노드보다 작다.
        }
        
        public String toString()
        {
            return x + " " + y + " " + val;
        }
    }
}
```

# 23.02.13(월)
* 트리 구현을 알고리즘 공부하면서 처음 해보았다.
* 이제는 트리 문제도 많이 풀어봐야 할 것 같다.