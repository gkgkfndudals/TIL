# upper_bound, lower_bound

### 구현 할 때 주의사항과 팁
자바에서는 upper_bound, lower_bound를 직접 구하여야 한다.  

#### lower_bound
1. 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다.
2. 최대값과 같거나 보다 작은 값이 들어오면 그냥 index를 리턴해주면 된다.
3. 최소값 보다 더 작은 값이 들어오면 0을 리턴해주면 되므로 그냥 index를 리턴해주면된다.
  
ex) 
arr = {1, 2, 2, 3} 일때
lower_bound(arr, 4) => 4 출력
lower_bound(arr, -1) => 0 출력
  
#### upper_bound
1. 최대값과 같거나 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다.
2. 최대값보다 작은 값이 들어오면 그냥 index를 리턴해주면 된다.
3. 최소값 보다 더 작은 값이 들어오면 0을 리턴해주면 되므로 그냥 index를 리턴해주면된다.
  
ex)
arr = {1, 2, 2, 3} 일때
upper_bound(arr, 4) => 4 출력
upper_bound(arr, -1) => 0 출력

참고로 lower_bound는 upper_bound를 구하면 쉽게 구할 수가 있다.
```java
    static int lower_bound(int arr, int target)
    {
        // upper_bound에 target - 1을 해주면서 
        // lower_bound의 target의 위치를 찾을 수 있다.
        upper_bound(arr, target - 1); 
    }
```
  
CODE1는 좋지 않은 구현이다. right를 행렬의 index 끝으로 하면 이진탐색이 돌지 못하여 여러 문제가 생긴다.
 1. upper_bound에서 arr = {10} 이고 target >= 10 값으로 들어왔을때 return right가 0으로 반환된다.
 2. lower_bound에서도 더 큰 값이 들어왔을 경우 index + 1 을 해줘서 넘겨줘야된다. 그런데 arr = {10} 이고 target > 10 값으로 들어왔을때 return right가 0으로 반환된다.
 3. arr.size() == 1 일 경우 => 이진탐색을 돌지 않고 바로 right = 1 - 1 이 리턴 되므로 문제가 생긴다.  
 
**무조건 right = arr.size()로 해주자. 그러면 이진탐색이 적어도 1번은 무조건 돌면서 위의 문제들이 해결되고, 밑에 if문으로 예외적인 상황에 대해서 처리를 안하여도 된다.**  

CODE1
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
