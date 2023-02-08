# 백준 2798 - 블랙잭
https://www.acmicpc.net/problem/2798

### 이 문제를 풀기 위한 과정
조합 문제이다.

CODE1
```java
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.util.StringTokenizer;

    public class Main {
        static int N, M;
        static int[] arr;
        static int[] brr;
        static int answer = Integer.MIN_VALUE;
        
        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringTokenizer st= new StringTokenizer(br.readLine());
            
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());
            
            arr = new int[N];
            brr = new int[3];
            
            st = new StringTokenizer(br.readLine());
            for(int i = 0; i < N; i++)
            {
                arr[i] = Integer.parseInt(st.nextToken());
            }
            
            combi(0, 0);
            
            System.out.println(answer);
        }
        
        static void combi(int depth, int start)
        {
            if(depth == 3)
            {
                int sum = 0;
                for(int i = 0 ; i < brr.length; i++)
                {
                    sum += brr[i];
                }
                
                if(sum <= M)
                {
                    answer = Math.max(answer, sum);				
                }
                
                return;
            }
            
            for(int i = start; i < N; i++)
            {
                brr[depth] = arr[i];
                combi(depth + 1, i + 1);
            }
        }

    }


```

# 23.02.08(화)
* 
