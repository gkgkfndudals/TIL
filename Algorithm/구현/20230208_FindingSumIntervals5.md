# 백준 11660 - 구간 합 구하기5
https://www.acmicpc.net/problem/11660

### 이 문제를 풀기 위한 과정
2차원을 1차원으로 만들어서 풀었는데, 생각해보니 굳이 1차원으로 만들 필요가 없었다.  

1. 입력과 동시에 sum을 해주어 배열에 저장한다.
2. 행 별로 뒤에서 앞으로 빼주어 구간 누적 합을 구한다.

CODE1
```java
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.util.StringTokenizer;

    public class Main {
        static int N, M;
        static int[] arr;
        static int answer = 0;

        public static void main(String[] args) throws Exception {
            StringBuilder sb = new StringBuilder();
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringTokenizer st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());

            arr = new int[N * N];

            int sum = 0;
            for (int i = 0; i < N; i++) {
                st = new StringTokenizer(br.readLine());
                for (int j = 0; j < N; j++) {
                    sum += Integer.parseInt(st.nextToken());
                    arr[i * N + j] = sum;
                }
            }

            for (int i = 0; i < M; i++) {
                int x1, y1, x2, y2;
                st = new StringTokenizer(br.readLine());
                x1 = Integer.parseInt(st.nextToken()) - 1;
                y1 = Integer.parseInt(st.nextToken()) - 1;
                x2 = Integer.parseInt(st.nextToken()) - 1;
                y2 = Integer.parseInt(st.nextToken()) - 1;

                answer = solution(x1, y1, x2, y2);
                sb.append(answer).append("\n");
            }

            System.out.println(sb.toString());
        }

        static int solution(int x1, int y1, int x2, int y2) {
            int ans = 0;

            for (int i = x1; i <= x2; i++) {
                int end = i * N + y2;
                int start = i * N + y1 - 1;

                int rowSum = 0;
                if (start < 0) {
                    rowSum = arr[end];
                } else {
                    rowSum = arr[end] - arr[start];
                }
    //			System.out.println(i+"번째: " + rowSum);
                ans = ans + rowSum;
            }

            return ans;
        }
    }

```

# 23.02.08(화)
* 
