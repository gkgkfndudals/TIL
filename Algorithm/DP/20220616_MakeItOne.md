# 백준 - 1로 만들기

### 이 문제를 풀기 위한 과정
시간 복잡도 O(N)으로 bottom-up 방식으로 for문을 사용해서 풀었다.

문제에서 요구하는 내용을 점화식으로 표현하면  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220619_MakeItOne2.PNG) 

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220619_MakeItOne1.PNG) 이 나온다.


CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(int X);

    int main(void)
    {
        int X;

        cin >> X;

        int answer = solution(X);

        cout << answer;
        return 0;
    }

    int solution(int X)
    {
        int answer = 0;

        vector<int> dp;
        dp.assign(30001, 0);

        for (int i = 2; i <= X; i++)
        {
            dp[i] = dp[i - 1] + 1;

            if (i % 2 == 0)
            {
                dp[i] = min(dp[i], dp[i / 2]+1);
            }
            if (i % 3 == 0)
            {
                dp[i] = min(dp[i], dp[i / 3]+1);
            }
            if (i % 5 == 0)
            {
                dp[i] = min(dp[i], dp[i / 5]+1);
            }
        }

        return dp[X];
    }
    

# 22.06.16(목))
* DP문제는 문제를 보고 점화식만 구하면 문제를 풀 수 있는데, 아직 DP 문제를 많이 풀어보지 않아 너무 어렵다.... 꾸준히 DP문제를 풀어봐야 될 것 같다.