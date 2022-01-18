# 백준 - 연구소

### 이 문제를 풀기 위한 과정
이 문제는 벽 세우는 시간 복잡도 n*mC3이다. 
벽의 개수가 3개가 되는 모든 조합을 찾은 뒤에 그러한 조합에 대해서 DFS, BFS로 바이러스를 퍼트린 후 안전 영역의 크기를 계산하면 된다.

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    void combination(int depth, int idx);
    int getSafeArea();
    void virusDFS(int x, int y);

    static int N, M;
    vector<vector<int>> map;
    int answer = 0;
    vector<pair<int, int>> virusPos;
    static int dir_x[] = { 0, -1, 0, 1 };
    static int dir_y[] = { -1, 0, 1, 0 };
    vector<vector<int>> temp;

    int main(void)
    {
        cin >> N >> M;
        map.assign(N, vector<int>(M));
        temp.assign(N, vector<int>(M));

        for (int i = 0; i < N; i++)
        {
            for(int j =0; j< M ; j++)
            {
                cin >> map[i][j];

                if (map[i][j] == 2)
                {
                    virusPos.push_back(make_pair(i, j));
                }
            }
        }
        

        combination(0, 0);

        cout << answer;

        return 0;
    }

    void combination(int depth, int idx)
    {
        if (depth == 3)
        {
            copy(map.begin(), map.end(), temp.begin());

            for (pair<int, int> p : virusPos)
            {
                virusDFS(p.first, p.second);
            }

            answer = max(answer, getSafeArea());

            return;
        }

        int x, y;
        for (int i = idx; i < M * N; i++)
        {
            x = i / M;
            y = i % M;

            if (map[x][y] == 0)
            {
                map[x][y] = 1;
                idx++;
                combination(depth + 1, idx);
                map[x][y] = 0;
            }
        }
    }

    int getSafeArea()
    {
        int cnt = 0;

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                if (temp[i][j] == 0)
                    cnt++;
            }
        }

        return cnt;
    }

    void virusDFS(int x, int y) 
    {
        int new_x, new_y;

        for (int i = 0; i < 4; i++)
        {
            new_x = x + dir_x[i];
            new_y = y + dir_y[i];

            if (new_x >= 0 && new_y >= 0 && new_x < N && new_y < M)
            {
                if (temp[new_x][new_y] == 0)
                {
                    temp[new_x][new_y] = 2;
                    virusDFS(new_x, new_y);
                }
            }
        }

        
    }


# 22.01.18화)
* 순열 next_permutation 을 이용하여 조합을 구현하여 문제를 풀으라고 했지만 불가능한걸 깨닫고 그냥 조합을 구현하여서 풀었다.
* 앞으로 그냥 N과 M문제 풀이으로 쓰인 순열, 조합을 이용하자