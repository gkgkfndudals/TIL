#  SWEA - 준환이의 양팔저울

### 이 문제를 풀기 위한 과정
1. 무게 weights의 올려놓을 순서를 순열로 구한다.
2. perm 배열에 실행완료 된 순열을 저장하여, 순열이 완성되었을 경우 오른쪽과 왼쪽중에 어디를 올리지를 정한다.
3. 현재 weight를 오른쪽에 올리는 경우, 왼쪽에 올리는 경우를 각각 재귀로 구한다.
4. 문제에서 항상 오른쪽 위에 올라가 있는 무게의 총합이 왼쪽에 올라가 있는 무게의 총합보다 더 커져서는 안 된다라는 조건 이있으므로 left < right 일때 return을 해준다.
5. 기저조건을 만족한 경우, 경우의 수 ans를 증가

CODE1

    import java.util.Scanner;
    import java.io.*;
    import java.util.*;

    class Solution {
        static int N;
        static int[] weights, perm;
        static boolean[] check;
        static int ans;

        public static void main(String args[]) throws Exception {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringBuilder sb = new StringBuilder();
            
            int T;
            T = Integer.parseInt(br.readLine());
            
            for (int test_case = 1; test_case <= T; test_case++) {
                N = Integer.parseInt(br.readLine());
                weights = new int[N];
                perm = new int[N];
                check = new boolean[N];

                StringTokenizer st = new StringTokenizer(br.readLine());
                for (int i = 0; i < N; i++) {
                    weights[i] = Integer.parseInt(st.nextToken());
                }

                ans = 0;
                permutation(0);
                sb.append("#").append(test_case).append(" ").append(ans).append("\n");
            }
            System.out.println(sb.toString());
            br.close();
        }

        static void permutation(int depth) {
            if (depth == N) {
                recursion(0, 0, 0);
            }

            for (int i = 0; i < N; i++) {
                if (check[i] == false) {
                    perm[depth] = weights[i];
                    check[i] = true;
                    permutation(depth + 1);
                    check[i] = false;
                }
            }
        }

        static void recursion(int idx, int left, int right) {
            if (left < right) {
                return;
            }

            if (idx == N) {
                ans++;
                return;
            }

            recursion(idx + 1, left + perm[idx], right);
            recursion(idx + 1, left, right + perm[idx]);
        }
    }
        
# 23.01.08(일)
* 순열과 재귀 함수를 이용한 문제이였다.
* 비슷한 문제로는 https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/DP/20221111_DoubleArmedScale.md 이 있다.