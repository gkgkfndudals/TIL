# 백준(삼성전자 SW 역량테스트) - 인구 이동(DFS)

### 이 문제를 풀기 위한 과정
모든 나라의 위치에서 상, 하, 좌, 우로 국경선을 열 수 있는지를 확인해야 한다. 
따라서 모든 나라의 위치에서 DFS/BFS를 수행하여 인접한 나라의 인구수를 확인한 뒤에, 가능하다면 국경선을 열고 인구 이동 처리를 진행하면 된다.



CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution();
    void DFS(int x, int y);

    int dir_x[] = { 0, -1, 0, 1 };
    int dir_y[] = { -1, 0, 1, 0 };

    int N, L, R;
    vector<vector<int>> map;
    vector<vector<bool>> visited;
    vector<pair<int, int>> vec;
    int cnt, sum;

    int main()
    {
        cin >> N >> L >> R;

        map.assign(N, vector<int>(N, 0));
        visited.assign(N, vector<bool>(N, false));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                cin >> map[i][j];
            }
        }

        int ans = solution();

        cout << ans;

        return 0;
    }

    int solution()
    {
        int ans = 0;

        while (1)
        {
            bool flag = false;
            visited.assign(N, vector<bool>(N, false));

            for (int i = 0; i < map.size(); i++)
            {
                for (int j = 0; j < map.size(); j++)
                {
                    vec.clear();

                    if (!visited[i][j])
                    {
                        cnt = 1;
                        visited[i][j] = true;
                        sum = map[i][j];
                        vec.push_back(make_pair(i, j));
                        DFS(i, j);


                        if (cnt > 1)
                        {
                            flag = true;
                            int avg = sum / cnt;

                            for (int k = 0; k < vec.size(); k++)
                            {
                                map[vec[k].first][vec[k].second] = avg;
                            }
                        }
                    }

                }
            }

            if (flag == false)
                break;
            else
                ans++;
        }



        return ans;

    }

    void DFS(int x, int y)
    {
        for (int i = 0; i < 4; i++)
        {
            int new_x, new_y;
            new_x = x + dir_x[i];
            new_y = y + dir_y[i];


            if (new_x >= 0 && new_y >= 0 && new_x < N && new_y < N)
            {
                if (!visited[new_x][new_y])
                {
                    if (abs(map[x][y] - map[new_x][new_y]) >= L && abs(map[x][y] - map[new_x][new_y]) <= R)
                    {
                        cnt++;
                        visited[new_x][new_y] = true;
                        sum += map[new_x][new_y];
                        vec.push_back(make_pair(new_x, new_y));
                        DFS(new_x, new_y);
                    }
                }
            }


        }
    }


# 22.04.22(금)
* 문제에서 제시한 답은 인구이동이 며칠 동안 발생하는지를 구하는 것이지만, 나는 단순 이중 for문으로 하루 치 인구이동을 계산하여 문제풀이 오류가 났었다.
이런 문제의 답에서는 무한루프로 한번 더 감싸줘야 된다고 꼭 기억하자.
그리고 visited의 위치도 주의하자. 실수가 은근 많았다.