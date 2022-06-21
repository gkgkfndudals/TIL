#  알고리즘 - 바닥 공사(나동빈 책)

### 이 문제를 풀기 위한 과정

왼쪽부터 차례대로 바닥을 덮개로 채운다고 생각하면 어렵지 않게 점화식을 세울 수 있다.

이 문제에서 N-2 미만의 길이에 대해서는 고려할 필요가 없다. 왜냐하면 사용할 수 있는 덮개의 형태가 최대 2 X 2의 직사각형 형태이기 때문이다. 다시 말해 바닥을 채울 수 있는 형태는 위에서 언급한 경우밖에 없다.

1. 왼쪽부터 i - 1까지 길이가 덮개로 이미 채워져 있으면 2 x 1 덮개를 채우는 하나의 경우밖에 존재하지 않는다.
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction1.PNG)

2. 왼쪽부터 i - 2까지 길이가 덮개로 이미 채워져 있으면 1 x 2 덮개 2개를 넣는 경우, 혹은 2 x 2의 덮개 하나를 넣는 경우로 2가지 경우가 존재한다.
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction2.PNG) 

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220622_FloorConstruction3.PNG) 

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

        return 0;
    }

    int solution(int N)
    {
        int answer = 0;

        int dp[1001];

        dp[1] = 1;
        dp[2] = 3;

        for (int i = 3; i < N; i++)
        {
            dp[i] = (dp[i - 1] + 2 * dp[i - 2]) % 796796; //796796으로 나눠라고 문제에 제시되어있다.
        }

        return answer;
    }
    

# 22.06.19(일)
* 역시 점화식을 구하는게 너무 어려워서 답안을 봤다.
* 처음에는 dp[i], dp[i+2] 이렇게 '+' 으로 점화식을 생각하였는데 점화식을 도저히 못 구하였다. 하지만 답안에서 인덱스를 '-' 으로 점화식을 구하는 아이디어를 보고 감탄을 하였다. 이 문제를 다시한번 꼭 풀어보고 이런 생각의 전환을 연습해야 되겠다.