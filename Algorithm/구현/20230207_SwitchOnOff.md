# 백준 1244 - 스위치 켜고 끄기
https://www.acmicpc.net/problem/1244
  
### 이 문제를 풀기 위한 과정

CODE1
```java
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.util.StringTokenizer;

    public class SwitchOnOff {
        static int N;
        static int[] arr;
        static int M;

        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            N = Integer.parseInt(br.readLine());
            arr = new int[N + 1];

            StringTokenizer st = new StringTokenizer(br.readLine());
            for (int i = 1; i < N + 1; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }
            M = Integer.parseInt(br.readLine());

            for (int m = 0; m < M; m++) {
                st = new StringTokenizer(br.readLine());
                int gender = Integer.parseInt(st.nextToken());
                int num = Integer.parseInt(st.nextToken());

                if (gender == 1) {
                    for(int i = 1; i <= N; i++)
                    {
                        if(i % num == 0)
                        {
                            arr[i] = arr[i] == 0 ? 1:0;
                        }
                    }
                } else {
                    arr[num] = arr[num] == 0 ? 1:0;
                    
                    for(int i = 1; i <= N; i++)
                    {
                        if(num - i <= 0 || num + i > N)
                        {
                            break;
                        }
                        
                        if(arr[num - i] == arr[num + i])
                        {
                            arr[num - i] = arr[num - i] == 0 ? 1: 0;
                            arr[num + i] = arr[num + i] == 0 ? 1: 0;
                        } else {
                            break;
                        }
                    }
                }
            }
            
            for(int i = 1 ; i <= N; i++)
            {
                System.out.print(arr[i] + " ");
                if(i % 20 == 0) {
                    System.out.println();
                }
            }
        }

    }

```

# 23.02.07(화)
* 
