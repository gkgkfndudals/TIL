#  이코테 - 편집 거리

### 이 문제를 풀기 위한 과정
2차원 배열을 통해 문자열을 하나 하나씩 비교를 해나간다.  
문자열 MICROSOFT와 NCSOFT를 비교한다고 하자. 모든 연속 부분 집합에 대해서 비교를 해야한다.  

1. 먼저 두 문자열의 처음 비교 대상은 공집합 두개이다. 둘다 같은 문자열이기 때문에 바꿀 것이 없어 비용은 0이다.  

2. 그 다음은 N과 {}이 되려면 하나를 추가 해야한다. 따라서 비용은 1이다.  
이어서 NC와 {}은 두개를 추가해야되기 때문에 비용은 2가 된다.  
따라서 문자열 길이 만큼 테이블 비용을 채워 주면 된다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220713_EditDistance1.PNG)

3. 다음 M과 N 을 비교해보자. 이 둘은 다르다. 따라서 값을 변경해야 한다. 코스트는 1이다.    
이어서 M과 NC. 둘다 다르고, 하나를 지우고 하나를 바꿔야 한다. 코스트는 2이다.  
M과 NCS. 셋 다 다르고 두개를 지우고 하나를 바꿔야 한다. 코스트는 3이다.

4. 문자열 M과 NC를 비교한다고 가정해보자. 여기서 M과 N은 이미 순차적으로 비교를 한 상태이다.  
만약 M과 C이 같다고 할때, 비용을 바꿔줄 필요가 없다. M과 N을 비교했던 값을 가져오기만 하면 된다.  
그리고 만약 M과 C 다를 경우엔, M과 N을 비교했던 값에서 비용을 하나 증가시켜 준다.  
    + MICROSOFT와 NCSOFT 마지막 T끼리 비교했을 때, 같으므로 MICROSOF와 NCSOF의 편집거리를 가져오면 된다.  
    + MICRO와 NCS를 비교 할 경우, O와 S는 서로 다르므로, MICR과 NC를 비교했을때의 비용에서 1을 증가시키면 된다.  

**따라서 A[i] == B[j] 일때의 편집거리 DP[i][j] = DP[i-1][j-1] 이다.**  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220713_EditDistance2.PNG)

5. 두 문자가 다를 경우, 이전의 편집거리에서 1을 증가시켜야 한다고 했다.  
MI와 NCS를 비교한다고 해보자. 총 3가지의 경우(대각선 위, 위, 왼쪽)의 수가 있다.  
    + 대각선 M과 NC의 편집거리를 가져오는 것은 I를 S로 수정하는 것이다. 즉 수정하면서 문자가 같으니 M과 NC를 비교한 편집 거리 + 수정 비용 1 을 더하면 된다.  
    + 위쪽인 M과 NCS의 편집거리에서 1을 증가시켜 MI, NCS 편집거리에서 I를 삭제한다는 것을 뜻한다. 즉 M과 NCS의 편집거리 + I를 삭제한 비용 1 더하면 된다.  
    + 마지막으로 왼쪽인 MI와 NC의 편집거리에서 1을 증가시켜 값을 MI, NCS 편집거리에 넣는다는 것은, MI뒤에 문자를 하나 추가한다는 것이다. 즉 MI뒤에 문자열을 하나 추가시켜 MIS, NCS이므로 MI, NC의 편집거리 + 추가 비용 1 더하면 된다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220713_EditDistance3.PNG)

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