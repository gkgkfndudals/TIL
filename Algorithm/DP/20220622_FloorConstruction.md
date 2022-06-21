#  알고리즘 - 바닥 공사(나동빈 책)

### 이 문제를 풀기 위한 과정

왼쪽부터 차례대로 바닥을 덮개로 채운다고 생각하면 어렵지 않게 점화식을 세울 수 있다.

이 문제에서 N-2 미만의 길이에 대해서는 고려할 필요가 없다. 왜냐하면 사용할 수 있는 덮개의 형태가 최대 2 X 2의 직사각형 형태이기 때문이다.

1. 왼쪽부터 i - 1까지 길이가 덮개로 이미 채워져 있으면 2 x 1 덮개를 채우는 하나의 경우밖에 존재하지 않는다.  
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction1.PNG)

2. 왼쪽부터 i - 2까지 길이가 덮개로 이미 채워져 있으면 1 x 2 덮개 2개를 넣는 경우, 혹은 2 x 2의 덮개 하나를 넣는 경우로 2가지 경우가 존재한다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction2.PNG) 

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction3.PNG) 

왼쪽부터 N - 2까지 길이가 덮개로 이미 채워져 있는 경우 덮개를 채우는 방법은 2가지 경우가 있다. 이 두 방법은 서로 다른 것이므로, 결과적으로는 dp[i] = dp[i-1] + dp[i-2] + dp[i-2]가 된다.  
따라서 dp[i] = dp[i-1] + dp[i-2]*2의 점화식이 나온다.  

CODE1

    #include <iostream>
    #include <vector>
    using namespace std;

    int solution(int N);

    int main(void)
    {
        int N;

        cin >> N;

        int answer = solution(N);

        return 0;
    }

    int solution(int N)
    {
        int answer = 0;

        int dp[1001];

        dp[1] = 1;
        dp[2] = 3;

        for (int i = 3; i < N; i++)
        {
            dp[i] = (dp[i - 1] + 2 * dp[i - 2]) % 796796; //796796으로 나눠라고 문제에 제시되어있다.
        }

        return answer;
    }
    

# 22.06.19(일)
* 타일 DP 문제는 옛날에도 몇 번 풀어봐서 그나마 쉽게 점화식을 세울 수 있었다.
* N = 3 일때 까지만 그림을 그려보면 금방 점화식을 세울 수 있다.