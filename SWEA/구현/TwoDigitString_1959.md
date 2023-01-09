#  SWEA - 두 개의 숫자열

### 이 문제를 풀기 위한 과정


CODE1

    import java.util.*;
    import java.io.*;

    class Solution {
        static int N, M;
        static int[] a = new int[N];
        static int[] b = new int[M];
        
        public static void main(String args[]) throws Exception {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringBuilder sb = new StringBuilder();

            int T;
            T = Integer.parseInt(br.readLine());

            for (int test_case = 1; test_case <= T; test_case++) {
                int ans = Integer.MIN_VALUE;
                StringTokenizer st = new StringTokenizer(br.readLine());

                N = Integer.parseInt(st.nextToken());
                M = Integer.parseInt(st.nextToken());
                a = new int[N];
                b = new int[M];

                st = new StringTokenizer(br.readLine());
                for (int i = 0; i < N; i++) {
                    a[i] = Integer.parseInt(st.nextToken());
                }
                st = new StringTokenizer(br.readLine());
                for (int i = 0; i < M; i++) {
                    b[i] = Integer.parseInt(st.nextToken());
                }

                if (N < M) {
                    int[] temp;
                    temp = a;
                    a = b;
                    b = temp;
                }

                
                for (int i = 0; i <= a.length - b.length; i++) {
                    int sum = 0;
                    for (int j = 0; j < b.length; j++) {
                        
                        sum = sum + a[i + j] * b[j];
                    }
                    if (sum >= ans) {
                        ans = sum;
                    }
                }

                sb.append("#" + test_case + " " + ans + "\n");
            }
            System.out.println(sb);
        }

    }
        
# 23.01.10(월)
* 