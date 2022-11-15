#  백준 - 양팔저울

### 이 문제를 풀기 위한 과정
이 문제는 물건을 쪼갤 수 없는 배낭문제(0/1 Knapsack Problem)이므로 DP로 풀어야한다.  

dp[x][y] : x번까지의 추를 사용했을 때 y 무게를 만들 수 있는지에 대한 여부 

i번째의 무게추를 
1. 왼쪽 저울에 올릴 것인지
2. 오른쪽 저울에 올릴 것인지
3. 아니면 아무것도 하지 않을 것인지
총 3가지 경우에 대해서 재귀로 구하여 주면 된다.  
 
오른쪽저울 - 왼쪽저울의 절대값으로 구슬의 무게를 구하면 된다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20221111_DoubleArmedScale1.png)  

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    void solution(int i, int w);

    bool dp[31][15001];
    int N, M;
    vector<int> weight, bead;

    int main()
    {
        weight.assign(31, 0);

        cin >> N;
        for (int i = 0; i < N; i++)
        {
            int num;
            cin >> num;
            weight[i] = num;
        }

        cin >> M;
        for (int i = 0; i < M; i++)
        {
            int num;
            cin >> num;
            bead.push_back(num);
        }

        solution(0, 0);

        for (int i = 0; i < bead.size(); i++)
        {
            if (bead[i] > 15000)
                cout << "N ";
            else if (dp[N][bead[i]] == true)
                cout << "Y ";
            else
                cout << "N ";
        }

        return 0;
    }

    void solution(int i, int w)
    {
        if (i > N || dp[i][w])
        {
            return;
        }

        dp[i][w] = true;

        solution(i + 1, w + weight[i]);
        solution(i + 1, abs(w - weight[i]));
        solution(i + 1, w);
    }

    /*
    2
    1 4
    2
    3 2
    */

# 22.11.11(금)
* 재귀를 이용해서 푸는 DP-Knapsack 문제였다.  
* 다음에 다시 한번 풀어보도록 하자
