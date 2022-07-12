#  이코테 - 못생긴 수

### 이 문제를 풀기 위한 과정
가능한 못생긴 수를 앞에서부터 하나씩 찾는 방법으로 해결 할 수 있다.  
못생긴 수에 2,3,5를 곱한 수 또한 '못생긴 수'에 해당된다.  
  
1. 2의 배수 변수, 3의 배수 변수, 5의 배수 변수에 대하여 각각 '가장 작은 못생긴 수'부터 오름차순으로 하나씩 확인한다.
2. 각 배수를 곱한 값도 '못생긴 수'가 될 수 있도록 처리하면 정답 판정을 받을 수 있다.

* 2의 배수 1 x 2 = 2, 3의 배수 1 x 3 = 3, 5의 배수 1 x 5 = 5
* 2의 배수 2 x 2 = 4, 3의 배수 2 x 3 = 6, 5의 배수 2 x 5 = 10

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

        cout << answer;
    }

    int solution(int N)
    {
        int answer = -1;

        int dp[1001];
        dp[0] = 0;
        dp[1] = 1;

        int next2 = 2;
        int next3 = 3;
        int next5 = 5;

        int idx2 = 1;
        int idx3 = 1;
        int idx5 = 1;

        for (int i = 2; i <= N; i++)
        {
            dp[i] = min(min(next2, next3), next5 );

            if (dp[i] == next2)
            {
                idx2++;
                next2 = dp[idx2] * 2;
            }
            if (dp[i] == next3)
            {
                idx3++;
                next3 = dp[idx3] * 3;
            }
            if (dp[i] == next5)
            {
                idx5++;
                next5 = dp[idx5] * 5;
            }
        }

        answer = dp[N];

        return answer;
    }

# 22.07.12(화)
* 문제의 이해를 잘못하여 점화식을 못 구해 풀지 못하였다.