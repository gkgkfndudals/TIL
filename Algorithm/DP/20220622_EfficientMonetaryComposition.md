#  알고리즘 - 효율적인 화폐 구성(나동빈 책)

### 이 문제를 풀기 위한 과정
이 문제는 그리디에서 다루었던 거스름돈 문제와 거의 동일하다. 하지만 화폐 단위에서 큰 단위가 작은 단위의 배수가 아니라서 그리디로는 문제를 해결 할 수 없다.

적은 금액부터 큰 금액까지 확인하며 차례대로 만들 수 있는 최소한의 화폐 개수를 찾으면 된다.  

금액 i를 만들 수 있는 최소한의 화폐 개수를 dp[i], 화폐의 단위를 k라고 했을때  
1. dp[i-k]를 만드는 방법이 존재하는 경우, dp[i] = min(dp[i], dp[i-k] + 1)
2. dp[i-k]를 만드는 방법이 존재하지 않는 경우, dp[i] = 10001

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    int solution(vector<int> v, int M);

    int main(void)
    {
        int N, M;
        vector<int> v;

        cin >> N >> M;

        for (int i = 0; i < N; i++)
        {
            int num;
            cin >> num;
            v.push_back(num);
        }

        int answer = solution(v, M);

        cout << answer;

        return 0;
    }

    int solution(vector<int> v, int M)
    {
        int answer = -1;
        int dp[10001];
        fill(dp, dp + 10001, 10001);

        dp[0] = 0;

        for (int i = 1; i < M+1; i++)
        {
            for (int j = 0; j < v.size(); j++)
            {
                int k = v[j];
                if (i - v[j] >= 0) 
                {
                    dp[i] = min(dp[i], dp[i - k] + 1);
                }
            }
        }

        if (dp[M] == 10001)
            dp[M] = -1;

        return dp[M];
    }

# 22.06.22(수)
* 이러한 유형의 문제는 코테에서 자주 봤었던 것으로 기억한다. 그리디 문제인 것 처럼 보이지만 그리디 문제로는 풀 수가 없다.
* 인상적인 부분은 만약 6원ㅇ르 만들기 위해 2원 화폐를 사용하는 최소 화폐 개수 dp[6]을 구하는 방식을 dp[6] = dp[6-2] + 1으로, 여기서 +1이 2원 화폐를 '한 번' 사용한 것을 의미한다.
* 나중에 꼭 다시 한번 이 문제를 풀어보도록 하자