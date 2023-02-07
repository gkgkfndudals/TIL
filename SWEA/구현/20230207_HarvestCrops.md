# SWEA 2805 - 농작물 수확하기
https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV7GLXqKAWYDFAXB
  
### 이 문제를 풀기 위한 과정
간단한 구현 문제이다.  
https://bingbing-study.tistory.com/10  
이렇게 하단부 구현을 할 수도 있다. 이게 더 편하고 좋은 것 같다.

CODE1
```java
    import java.util.LinkedList;
    import java.util.Queue;
    import java.util.Scanner;
    import java.util.StringTokenizer;
    import java.io.BufferedReader;
    import java.io.FileInputStream;
    import java.io.InputStreamReader;

    class Solution {
        static boolean[][] check;
        static int N;
        static int[] dir_x = {-1, 0, 1, 0};
        static int[] dir_y = {0, 1, 0, -1};
        
        public static void main(String args[]) throws Exception {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            int T = Integer.parseInt(br.readLine());
            StringBuilder sb = new StringBuilder();
            
            for (int test_case = 1; test_case <= T; test_case++) {
                int answer = 0;
                N = Integer.parseInt(br.readLine());
                int[][] arr = new int[N][N];
                check = new boolean[N][N];
                
                for (int i = 0; i < N; i++) {
                    String input = br.readLine();
                    for (int j = 0; j < N; j++) {
                        int num = input.charAt(j) - '0';
                        arr[i][j] = num;
                    }
                }
                
                for(int i = 0; i <= N/2; i++) // 상단부 가운데 포함
                {
                    for(int j = N/2 - i; j <= N/2 + i; j++ )
                    {
                        answer += arr[i][j];
                    }
                }
                
                for(int i = N/2 + 1 ; i < N ; i++) // 하단부
                {
                    for(int j = i - N/2; j < N - i + N/2; j++)
                    {
                        answer += arr[i][j];
                    }
                }
                
                sb.append("#").append(test_case).append(" ").append(answer).append("\n");
            }
            
            System.out.println(sb.toString());
        }
    }
```

# 23.02.07(화)
* 
