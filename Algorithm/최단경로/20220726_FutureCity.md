#  이코테 - 미래 도시

### 이 문제를 풀기 위한 과정
이 문제는 전형적인 플로이드 워셜 알고리즘 문제이다. 현재 문제에서 N의 범위가 100 이하로 매우 한정적이다. 따라서 플로이드 워셜 알고리즘을 이용해도 O(N^3) 10^3 이므로 구현이 간단한 플로이드 워셜 알고리즘을 이용하는 것이 유리하다.  

**DP[i][j] = min(DP[i][k], DP[i][k] + DP[k][j])**

1. 이 문제의 핵심 아이디어는 1번 노드에서 X를 거쳐 K로 가는 최단 거리는 (1번 노드 -> K 까지의 최단 거리 + K노드 -> X까지의 최단 거리) 이다.  
2. 2차원 배열에 열과 행이 같은 곳은 0으로 초기화 시켜준다. 
3. 그리고 간선이 양방향이므로 각각 1으로 초기화 해준다.  
4. 플로이드 워셜로 2차원 배열 map의 값을 모두 구한 뒤, map[1][K] + map[K][X]의 값을 구한다.

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(vector<vector<int>> map);

    int N, M;
    int K, X;

    int main(void)
    {
        cin >> N >> M;
        vector<vector<int>> map;
        map.assign(N+1, vector<int>(N+1, 1e9));

        for (int i = 0; i < N+1; i++)
        {
            for (int j = 0; j < N+1; j++)
            {
                if (i == j)
                {
                    map[i][j] = 0;
                }
            }
        }

        for (int i = 0; i < M; i++)
        {
            int e1, e2;
            cin >> e1 >> e2;
            map[e1][e2] = 1;
            map[e2][e1] = 1;
        }

        cin >> X >> K;

        int answer = solution(map);

        cout << answer;
    }

    int solution(vector<vector<int>> map)
    {
        int answer = -1;

        for (int k = 1; k < N+1; k++)
        {
            for (int i = 1; i < N+1; i++)
            {
                for (int j = 1; j < N+1; j++)
                {
                    map[i][j] = min(map[i][j], map[i][k] + map[k][j]);
                }
            }
        }

        int result = map[1][K] + map[K][X];

        if (result >= 1e9)
            answer = -1;
        else
            answer = result;

        return answer;
    }

    /*
    5 7
    1 2
    1 3
    1 4
    2 4
    3 4
    3 5
    4 5
    4 5
    */

    /*
    4 2
    1 3
    2 4
    3 4
    */

# 22.07.26(화)
* 플로이드 워셜의 전형적인 문제였다.  
* DP[i][j] = min(DP[i][k], DP[i][k] + DP[k][j]) 이것만 잘 기억하자