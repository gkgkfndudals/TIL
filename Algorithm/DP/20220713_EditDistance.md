#  이코테 - 편집 거리

### 이 문제를 풀기 위한 과정
2차원 배열을 통해 문자열을 하나 하나씩 비교를 해나간다.  
문자열 MICROSOFT와 NCSOFT를 비교한다고 하자. 모든 연속 부분 집합에 대해서 비교를 해야한다.  

+ 먼저 두 문자열의 처음 비교 대상은 공집합 두개이다. 둘다 같은 문자열이기 때문에 바꿀 것이 없어 비용은 0이다.  

- 그 다음은 N과 {}이 되려면 하나를 추가 해야한다. 따라서 비용은 1이다.  
이어서 NC와 {}은 두개를 추가해야되기 때문에 비용은 2가 된다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220713_EditDistance1.PNG)




CODE1

    #include <iostream>
    #include <vector>
    #include <string>

    using namespace std;

    int solution(string A, string B);

    int main(void)
    {
        string A, B;
        cin >> A >> B;

        int answer = solution(A, B);

    }

    int solution(string A, string B)
    {
        int answer = -1;

        int lenA = A.length() + 1;
        int lenB = B.length() + 1;

        vector<vector<int>> dp;
        dp.assign(lenA, vector<int>(lenB));
        
        for (int i = 0; i < lenA; i++)
        {
            dp[i][0] = i;
        }

        for (int j = 0; j < lenB; j++)
        {
            dp[0][j] = j;
        }

        for (int i = 1; i < lenA; i++)
        {
            for (int j = 1; j < lenB; j++)
            {
                if (A[i - 1] == B[j - 1])
                {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                else
                {
                    dp[i][j] = min(dp[i - 1][j] + 1, dp[i][j - 1] + 1);
                    dp[i][j] = min(dp[i - 1][j - 1] + 1, dp[i][j]);
                }
            }
        }


        for (int i = 0; i < lenA; i++)
        {
            for (int j = 0; j < lenB; j++)
            {
                cout << dp[i][j] << " ";
            }

            cout << endl;
        }
        return answer;
    }

# 22.07.12(화)
* 문제의 이해를 잘못하여 점화식을 못 구해 풀지 못하였다.