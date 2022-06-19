#  알고리즘 - 개미 전사(나동빈 책)

### 이 문제를 풀기 위한 과정
왼쪽부터 차례대로 식량창고를 턴다고 가정하여 점화식을 세운다.

1. (i - 1)번째 식량창고를 털기로 결정한 경우 현재의 식량창고를 털 수 없다.
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220619_AntWarrior1.PNG)

2. (i - 2)번째 식량창고를 털기로 결정한 경우 현재의 식량창고를 털 수 있다.
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220619_AntWarrior2.PNG) 

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(int N, vector<int> v);

    int main(void)
    {
        int N, K;
        vector<int> vec;

        cin >> N;

        for (int i = 0; i < N; i++)
        {
            cin >> K;
            vec.push_back(K);
        }

        int answer = solution(N, vec);

        cout << answer;
    }

    int solution(int N, vector<int> v)
    {
        int answer = 0;

        int dp[101];

        dp[0] = v[0];
        dp[1] = v[1];

        for (int i = 2; i < N; i++)
        {
            dp[i] = max(dp[i - 1], dp[i - 2] + v[i]);
        }

        answer = dp[N - 1];

        return answer;
    }
    

# 22.06.19(일)
* 역시 점화식을 구하는게 너무 어려워서 답안을 봤다.
* 처음에는 dp[i], dp[i+2] 이렇게 '+' 으로 점화식을 생각하였는데 점화식을 도저히 못 구하였다. 하지만 답안에서 인덱스를 '-' 으로 점화식을 구하는 아이디어를 보고 감탄을 하였다. 이 문제를 다시한번 꼭 풀어보고 이런 생각의 전환을 연습해야 되겠다.