# 백준 - 1로 만들기

### 이 문제를 풀기 위한 과정
시간 복잡도 O(N)으로 bottom-up 방식으로 for문을 사용해서 풀었다.

문제에서 요구하는 내용을 점화식으로 표현하면
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220619_MakeItOne1.png)


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
* 처음에는 if(cnt == C)라고 코드를 작성하였는데 틀렸다고 나왔다. 하지만 곰곰히 생각을 해보니 C개보다 많이 설치할 수 있다는 것은 곧 C개도 설치할 수 있음을 의미한다는 것을 볼 수 있습니다.  
이진탐색 알고리즘 연습하기에 좋은 문제라고 생각한다. 나중에 다시 한번 이 문제를 풀어보는 것이 좋을 것 같다.