#  백준 - 퇴사

### 이 문제를 풀기 위한 과정


CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(int N, vector<int> T, vector<int> P);
    int solutionTwo(int N, vector<int> T, vector<int> P);

    int main(void)
    {
        int N;
        vector<int> T, P;

        cin >> N;
        
        T.push_back(0);
        P.push_back(0);

        for (int i = 0; i < N; i++)
        {
            int num1, num2;
            cin >> num1 >> num2;
            T.push_back(num1);
            P.push_back(num2);
        }

        int answer = solutionTwo(N, T, P);

        cout << answer;
    }

    int solution(int N, vector<int> T, vector<int> P)
    {
        int answer = -1;
        
        int dp[16];
        fill(dp, dp + 16, 0);

        int deadline;

        for (int i = N; i > 0; i--)
        {
            deadline = i + T[i];
            
            if (deadline > N + 1)
            {
                dp[i] = dp[i + 1];
            }
            else
            {
                dp[i] = max(dp[i + 1], dp[deadline] + P[i]);
            }
        }


        return answer;
    }

    int solutionTwo(int N, vector<int> T, vector<int> P)
    {
        int answer = -1;

        int dp[16];
        fill(dp, dp + 16, 0);

        int deadline;

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j < i; j++)
            {
                dp[i] = max(dp[i], dp[j]);

                if (j + T[j] == i)
                {
                    dp[i] = max(dp[i], dp[j] + P[j]);
                }
            }

            answer = max(answer, dp[i]);
        }

        return answer;
    }

# 22.07.01(금)
* 