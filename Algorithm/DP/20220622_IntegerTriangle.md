#  알고리즘 - 금광(나동빈 책)

### 이 문제를 풀기 위한 과정
이 문제는 20220622_GoldMine(https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/DP/20220622_GoldMine.md) 과 매우 유사한 문제이다.

1. 왼쪽 위에서 오는 경우
2. 위에서 오는 경우

이렇게 2가지 위치에서만 내려올 수 있다. 따라서 모든 위치를 기준으로 이전 위치로 가능한 2가지 위치까지의 최적의 합 중에서 더 큰 합을 가지는 경우를 선택하면 된다.

vector 변수는 초기 '정수 삼각형' 정보를 담고 있으며, 2차원 dp 테이블이 있다.

* dp[i][j] = v[i][j] + max(dp[i-1][j-1], dp[i-1][j])

단, dp 테이블에 접근해야 할 때마다 리스트의 범위를 벗어나지 않는지 체크할 필요가 있다.

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>
    #include <cstring>

    using namespace std;

    int solution(vector<vector<int>> v, int N);

    int main(void)
    {
        int N;

        cin >> N;

        vector<vector<int>> v;

        for (int i = 0; i < N; i++)
        {
            vector<int> v2;
            for (int j = 0; j <= i; j++)
            {
                int num;
                cin >> num;
                v2.push_back(num);
            }

            v.push_back(v2);
        }

        int answer = solution(v, N);

        cout << answer;
    }

    int solution(vector<vector<int>> v, int N)
    {
        int answer = -1;

        int dp[500][500];

        memset(dp, -1, sizeof(dp));

        dp[0][0] = v[0][0];
        
        int up_left, up;

        for (int i = 1; i < v.size(); i++)
        {
            for (int j = 0; j < v[i].size(); j++)
            {
                if (j == 0)
                {
                    up_left = 0;
                }
                else
                {
                    up_left = dp[i - 1][j - 1];
                }

                if (j == i)
                {
                    up = 0;
                }
                else
                {
                    up = dp[i - 1][j];
                }
                
                dp[i][j] = v[i][j] + max(up_left, up);
            }
        }

        for (int j = 0; j < N; j++)
        {
            answer = max(answer, dp[N - 1][j]);
        }

        return answer;
    }

# 22.06.22(수)
* 20220622_GoldMine(https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/DP/20220622_GoldMine.md) 와 똑같은 문제였다.