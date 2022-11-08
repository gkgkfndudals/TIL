#  백준 - 수강 과목

### 이 문제를 풀기 위한 과정
이 문제는 물건을 쪼갤 수 없는 배낭문제(0/1 Knapsack Problem)이므로 DP로 풀어야한다.  

https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/DP/20221102_NomalKnapsack.md  
이 문제랑 완전 똑같은 문제이다.  

차이점은 vector의 v[0]을 빈공간으로 두지 않았기 때문에 점화식에서 v[i-1]로 했다.  

CODE1

    #include <iostream>
    #include <vector>
    using namespace std;

    struct item
    {
        int weight;
        int time;
    };

    int solution(int N, int K, vector<item> v);

    int main()
    {
        int N, K;

        cin >> N >> K;

        vector<item> v;

        for (int i = 0; i < K; i++)
        {
            int I, T;
            cin >> I >> T;

            v.push_back(item{ I, T });
        }

        int answer = solution(N, K, v);

        cout << answer;
        return 0;
    }

    int solution(int N, int K, vector<item> v)
    {
        vector<vector<int>> dp;
        dp.assign(K + 1, vector<int>(N + 1, 0));

        for (int i = 1; i <= K; i++)
        {
            for (int j = 1; j <= N; j++)
            {
                if (j >= v[i - 1].time)
                {
                    dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - v[i - 1].time] + v[i - 1].weight);
                }
                else
                {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }

        return dp[K][N];
    }

    /*
    80 3
    650 40
    700 60
    60 40
    */

# 22.11.08(화)
* 