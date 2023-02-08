# 백준 10816 - 숫자 카드2
https://www.acmicpc.net/problem/10816

### 이 문제를 풀기 위한 과정
이 문제는 upper_bound, lower_bound를 이용하면 쉽게 풀 수 있는 문제이다.  
Arrays.sort의 시간복잡도는 최대 n^2인데 통과가 되긴 하였다.  
  
참고로 lower_bound는 upper_bound를 구하면 쉽게 구할 수가 있었다...
```java
    static int lower_bound(int target)
    {
        upper_bound(target - 1);
    }
```

CODE1
```java
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.util.Arrays;
    import java.util.StringTokenizer;

    public class Main {
        static int N, M;
        static int[] arr, brr;
        
        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            StringBuilder sb = new StringBuilder();
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            N = Integer.parseInt(br.readLine());
            arr = new int[N];
            
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int i = 0; i < N; i++)
            {
                arr[i] = Integer.parseInt(st.nextToken());
            }
            
            M = Integer.parseInt(br.readLine());
            brr = new int[M];
            st = new StringTokenizer(br.readLine());
            for(int i = 0; i < M; i++)
            {
                brr[i] = Integer.parseInt(st.nextToken());
            }
            
            
            Arrays.sort(arr); // 오름차순
            
            for(int i = 0; i < M; i++) {
                int answer = solution(brr[i]);
                sb.append(answer).append(" ");
            }
            
            System.out.println(sb.toString());
        }
        
        static int solution(int card)
        {
            return upper_bound(card) - lower_bound(card);
        }
        
        static int lower_bound(int target)
        {
            int left = 0, right = N;
            
            while(left < right)
            {
                int mid = (left+right) / 2;
                
                if(arr[mid] < target)
                {
                    left = mid + 1;
                }
                else if(arr[mid] >= target){
                    right = mid;
                }
            }
        
            return right;
        }
        
        static int upper_bound(int target)
        {
            int left = 0, right = N;
            
            while(left < right)
            {
                int mid = (left + right) / 2;
                
                if(arr[mid] <= target)
                {
                    left = mid + 1;
                }
                else if(arr[mid] > target){
                    right = mid;
                }
            }
            
            return right;
        }
    }
```
  
CODE2
```java
    static int lower_bound(int target)
	{
		int left = 0, right = N-1;
		
		while(left < right)
		{
			int mid = (left+right) / 2;
			
			if(arr[mid] < target)
			{
				left = mid + 1;
			}
			else if(arr[mid] >= target){
				right = mid;
			}
		}
		
		if(arr[right] < target)
		{
			right++;
		}
		
		return right;
	}
	
	static int upper_bound(int target)
	{
		int left = 0, right = N-1;
		
		while(left < right)
		{
			int mid = (left + right) / 2;
			
			if(arr[mid] <= target)
			{
				left = mid + 1;
			}
			else if(arr[mid] > target){
				right = mid;
			}
		}
		
		if(arr[right] <= target)
		{
			right++;
		}
		
		return right;
	}
```


# 23.02.08(화)
* upper_bound, lower_bound 주의사항에 대해서 꼭 숙지하자.
