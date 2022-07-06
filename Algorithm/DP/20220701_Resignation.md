#  백준 - 퇴사

### 이 문제를 풀기 위한 과정
1. solution은 뒤에서 부터 계산을 하여 O(N)
2. solutionTwo는 앞에서 부터 계산을 하여 O(N^2)

이 문제를 풀 때는 뒤쪽 날짜부터 거꾸로 확인하는 방식으로 접근하여 해결 하는 방법이 있다.  
뒤쪽부터 매 상담에 대하여 '현재 상담 일자의 이윤(p[i]) + 현재 상담을 마친 일자부터의 최대 이윤(dp[t[i]+i])을 계산하면 된다. 이후에 계산된 각각의 값 중에서 최대값을 출력하면 된다.  
'dp[i] = i번째 날부터 마지막 날까지 낼 수 있는 최대 이익'이라고 하면  
dp[i] = max(p[i]+dp[t[i]+i], dp[i+1]) 이다.

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
* 앞에서 계산하였을 때 dp[i]를 구하기 위해서는 i까지 한번 더 for문을 돌려서 이중 반복문을 구현하여야 했지만, 뒤에서 계산하면 반복문 한번만으로 문제를 해결 할 수 있었다.
* 이런 비슷한 유형의 문제가 나온다면 과연 뒤에서 부터 계산한다는 생각을 할 수 있을지...
* 또한 앞에서 부터 계산하였을 때 구현 코드를 보면 LIS(최장 증가 수열) 알고리즘 조금 비슷한 것 같다.