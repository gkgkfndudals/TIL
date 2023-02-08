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
CODE2는 좋지 않은 구현이다. right를 행렬의 index 끝으로 하면 이진탐색이 돌지 못하여 여러 문제가 생긴다.
 1. upper_bound에서 arr = {10} 이고 target >= 10 값으로 들어왔을때 return right가 0으로 반환된다.
 2. lower_bound에서도 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다. 그런데 arr = {10} 이고 target > 10 값으로 들어왔을때 return right가 0으로 반환된다.

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
		
        // 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다.
		// 최대값과 같거나 보다 작은 값이 들어오면 그냥 index를 리턴해주면 된다.
		// 최소값 보다 더 작은 값이 들어오면 0을 리턴해주면 되므로 그냥 index를 리턴해주면된다.
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
		
        // 최대값과 같거나 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다.
		// 최대값보다 작은 값이 들어오면 그냥 index를 리턴해주면 된다.
		// 최소값 보다 더 작은 값이 들어오면 0을 리턴해주면 되므로 그냥 index를 리턴해주면된다.
		if(arr[right] <= target)
		{
			right++;
		}
		
		return right;
	}
```


# 23.02.08(화)
* upper_bound, lower_bound 주의사항에 대해서 꼭 숙지하자.
* https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/%EC%9D%B4%EC%A7%84%ED%83%90%EC%83%89/0_upper%2Clower%EA%B5%AC%ED%98%84%20%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD.md