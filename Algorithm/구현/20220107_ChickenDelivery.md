# 백준 - 치킨 배달

### 이 문제를 풀기 위한 과정
이 문제는 치킨집을 조합으로 M개를 정하여 도시의 치킨 거리의 합의 최솟값을 계산하면 되는 문제이다.

1. M <= 치킨 집의 개수 <= 13이므로  13CM 의 값은 100,000을 넘지않는다.
2. 집의 개수 또한 최대 100개이기 때문에, 완전탐색으로 문제를 해결 할 수 있다.

CODE1

    #include <iostream>
    #include <vector>
    #include <stdlib.h>
    #include <climits>

    using namespace std;

    int solution(vector<vector<int>> map, int M, vector<pair<int, int>> selChicken);
    void combination(int depth, int idx, vector<pair<int, int>> chicken);

    vector<vector<int>> map;
    int N, M;
    int answer = INT_MAX;
    vector<pair<int, int>> sel;


    int main(void)
    {
        cin >> N >> M;
        vector<pair<int, int>> chicken;

        map.assign(N, vector<int>(N));
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                cin >> map[i][j];

                if (map[i][j] == 2)
                {
                    chicken.push_back(make_pair(i, j));
                }
            }
        }

        combination(0, 0, chicken);

        cout << answer;
        
        return 0;
    }

    void combination(int depth, int idx, vector<pair<int, int>> chicken)
    {
        int min = 0;
        if (depth == M)
        {
            min = solution(map, M, sel);
            answer = min < answer ? min : answer;
            return;
        }

        for (int i = idx; i < chicken.size(); i++)
        {
            sel.insert(sel.begin() + depth, chicken.at(idx));
            sel.erase(sel.begin() + depth + 1, sel.end());
            idx++;
            combination(depth + 1, idx, chicken);
        }
    }

    int solution(vector<vector<int>> map, int M, vector<pair<int, int>> selChicken)
    {
        int min = 0;
        pair<int, int> p;

        for (int i = 0; i < map.size(); i++)
        {
            for (int j = 0; j < map.size(); j++)
            {
                if (map[i][j] == 1)
                {
                    int i_result = INT_MAX;

                    for (int k = 0; k < selChicken.size(); k++) 
                    {
                        p = selChicken[k];
                        int i_abs = abs(p.first - i) + abs(p.second - j);
                        i_result = (i_abs < i_result) ? i_abs : i_result;

                    }
                    
                    min += i_result;
                }
            }
        }

        return min;
    }





# 22.01.07(금)
* 전형적인 조합 문제이였다. 조합 문제를 많이 풀어봤지만 할때마다 조합의 depth, idx 구현에 헷갈려 시간을 날린다.
* 다시 N과 M의 문제를 복습할 필요가 있어보인다.