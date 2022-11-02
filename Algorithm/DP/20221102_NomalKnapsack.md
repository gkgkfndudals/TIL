#  백준 - 평범한 배낭

### 이 문제를 풀기 위한 과정
이 문제는 물건을 쪼갤 수 없는 배낭문제(0/1 Knapsack Problem)이므로 DP로 풀어야한다.  

1. 2차원 dp 행렬의 각 인덱스는 i -> i번째 물건, j -> 배낭 무게
2. 물건을 넣을 수 없는 경우에는 dp[i-1][j]의 값을 그대로 넣습니다.
3. 물건을 넣을 수 있는 경우에는 dp[i-1][j]의 값과 dp[i-1][j-w[i]] + v[i]의 값을 비교하여 더 큰 값을 넣습니다.

이 과정을 반복했을 때 dp[N][K]의 값이 가치의 최댓값이 됩니다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20221102_NomalKnapsack1.PNG)  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20221102_NomalKnapsack2.PNG)  

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    struct item
    {
        int weight;
        int value;
    };

    int solution(int N, int K, vector<item> vec);

    int main(void)
    {
        int N, K;
        cin >> N >> K;

        vector<item> v;
        v.assign(N + 1, item{ 0, 0 });
        for (int i = 1; i <= N; i++)
        {
            int V, W;
            cin >> W >> V;
            v[i] = item{ W, V };
        }

        int ans = solution(N, K, v);

        cout << ans;
    }

    int solution(int N, int K, vector<item> vec)
    {
        int answer = 0;

        vector<vector<int>> dp;
        dp.assign(N + 1, vector<int>(K + 1, 0));

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= K; j++)
            {
                if (j >= vec[i].weight)
                {
                    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - vec[i].weight] + vec[i].value);
                }
                else
                {
                    dp[i][j] = dp[i - 1][j];
                }

                cout << dp[i][j] << " ";
            }
            cout << endl;
        }

        answer = dp[N][K];
        return answer;
    }

    /*
    4 7
    6 13
    4 8
    3 6
    5 12
    */

# 22.11.02(수)
* 