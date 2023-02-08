# 백준 3040 - 백설 공주와 일곱 난쟁이
https://www.acmicpc.net/problem/3040

### 이 문제를 풀기 위한 과정
조합 문제이다.

CODE1
```java
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.util.Arrays;

    public class Main {
        static int[] arr;
        static int[] brr;
        static int[] answer;
        
        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            arr = new int[9];
            brr = new int[7];
            answer = new int[7];
            
            for(int i = 0; i < 9; i++)
            {
                arr[i] = Integer.parseInt(br.readLine());
            }
            
            combi(0, 0);
            
            for(int i = 0; i < answer.length; i++)
            {
                System.out.println(answer[i]);
            }
            
        }

        static void combi(int depth, int start) {
            if(depth == 7)
            {
                int sum = 0;
                for(int i =0 ; i < 7; i++)
                {
                    sum += brr[i];
                }
                
                if(sum == 100)
                {
                    answer = Arrays.copyOfRange(brr, 0, brr.length);
                }
                return;
            }
            
            for(int i = start; i < 9; i++)
            {
                brr[depth] = arr[i];
                combi(depth + 1, i + 1);
            }
        }
    }

```

# 23.02.08(화)
* 
