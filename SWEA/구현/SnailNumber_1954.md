# SWEA 1954 - 달팽이 숫자
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PobmqAPoDFAUq

### 이 문제를 풀기 위한 과정
1. N*N까지 반복문을 돌린다.
2. 새로운 x, y 값이 조건에 맞지 않다면 진행 방향을 바꿔주고 새로 값을 구해준다.
3. 방향대로 반복문의 i 값을 map 행렬에 저장한다.

CODE1
```java
    import java.util.Scanner;
    import java.util.StringTokenizer;
    import java.io.BufferedReader;
    import java.io.FileInputStream;
    import java.io.InputStreamReader;

    class Solution
    {
        static int[] dir_x = {0, 1, 0, -1};
        static int[] dir_y = {1, 0, -1, 0};
        
        public static void main(String args[]) throws Exception
        {
            StringBuilder sb = new StringBuilder();
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            int T = Integer.parseInt(br.readLine());

            for(int test_case = 1; test_case <= T; test_case++)
            {
                int N = Integer.parseInt(br.readLine());
                int[][] map = new int[N][N];
                
                int x = 0, y =0;
                int dir = 0;
                map[0][0] = 1;
                for(int i = 2; i <= N*N; i++)
                {
                    int new_x = dir_x[dir] + x;
                    int new_y = dir_y[dir] + y;
                    
                    if(new_x < 0 || new_y < 0 || new_x >= N || new_y >= N || map[new_x][new_y] != 0)
                    {	
                        dir++;
                        dir = dir % 4;
                        
                        new_x = dir_x[dir] + x;
                        new_y = dir_y[dir] + y;
                    }
                    x = new_x; 
                    y = new_y;
                    
                    map[new_x][new_y] = i;
                }
                
                sb.append("#").append(test_case).append("\n");
                for(int i = 0; i < N; i++)
                {
                    for(int j = 0; j < N; j++)
                    {
                        sb.append(map[i][j]).append(" ");
                    }
                    sb.append("\n");
                }
            }
            
            System.out.println(sb.toString());
        }
    }


```

# 23.02.08(화)
* 
