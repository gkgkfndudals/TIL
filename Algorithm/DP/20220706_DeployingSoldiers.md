#  백준 - 병사 배치하기

### 이 문제를 풀기 위한 과정
이 문제의 기본 아이디어는 LIS(최장 증가 수열) 알고리즘 문제이다. 
병사는 자신의 위치를 유지해야 하므로 따로 정렬을 하면 안되고, 그 안에서 내림차순으로 가는 가장 긴 수열을 찾아야 한다.  
이때 LIS는 최장 증가 부분 수열이지만 이 문제는 숫자가 감소하는 길이가 가장 긴 것을 찾아야 하므로 ' 
'최장 감소 부분 수열'을 찾으면 된다.  
LIS는 이중 for-loop을 사용하여 시간복잡도가 O(N^2)인 방법과 이분탐색을 이용하여 시간복잡도가 O(NlogN)인 방법이 있다. 이 문제는 N이 최대 2000이므로, O(N^2)의 시간복잡도를 가진 방법을 사용해도 무리가 없다.

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    int solution(int N, vector<int> v);

    int main(void)
    {
        int N;
        cin >> N;

        vector<int> v;

        for (int i = 0; i < N; i++)
        {
            int num;
            cin >> num;
            v.push_back(num);
        }

        int answer = solution(N, v);

        cout << answer;

    }

    int solution(int N, vector<int> v)
    {
        int answer = -1;

        int dp[2000];
        fill(dp, dp+2000, 1);

        for (int i = 1; i < N; i++)
        {
            for (int j = 0; j < i; j++)
            {
                if (v[j] > v[i])
                {
                    dp[i] = max(dp[j] + 1, dp[i]);
                }
            }
        }

        for (int i = 0; i < N; i++)
        {
            answer = max(dp[i], answer);
        }

        return N - answer;
    }

# 22.07.06(수)
* LIS 알고리즘은 3가지의 알고리즘이 있다.
* 그리디 O(2^N)
* DP O(N^2)
* 이진탐색 O(NlogN)