#  이코테 - 화성 탐사

### 이 문제를 풀기 위한 과정
이 문제는 (0, 0)의 위치에서 (N-1, N-1)의 위치로 이동하는 최단 거리를 계산하는 문제로 이해할 수 있다.  
따라서 N X N 크기의 맵이 주어졌을 때, 맵의 각 위치를 'node'로 보고, 상하좌우로 모든 노드가 연결되어 있다고 보면 된다. 예를 들어 위치 A와 위치 B가 서로 인접해 있다고 해보자. 이때  A -> B 로 가는 비용은 B 위치의 탐사 비용이 될 것이고, B -> A 로 가는 비용은 A 위치의 탐사 비용이 될 것이다.  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220810_MarsExploration1.PNG)
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220810_MarsExploration2.PNG)  

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220810_MarsExploration3.PNG)   

N의 범위 크기가 최대 125로 작다고 느낄 수 있지만, 2차원 공간이기 때문에 전체 노드의 개수는 N^2으로 10,000을 넘을 수 있다. 따라서 다익스트라 최단 경로 알고리즘을 이용해야 된다.  

CODE1

    #include <iostream>
    #include <vector>
    #include <queue>

    using namespace std;

    int solution(int N, vector<vector<int>> map);

    int dir_x[4] = { 0, -1, 0, 1 };
    int dir_y[4] = { -1, 0, 1, 0 };

    struct mars
    {
        int x;
        int y;
        int val;
    };

    struct cmp
    {
        bool operator()(mars& a, mars& b)
        {
            return a.val > b.val;
        }
    };

    int main(void)
    {
        int N;
        cin >> N;

        vector<vector<int>> map;
        map.assign(N, vector<int>(N, 0));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                int num;
                cin >> num;
                map[i][j] = num;
            }
        }

        int answer = solution(N, map);

        cout << answer;
    }

    int solution(int N, vector<vector<int>> map)
    {
        int answer = -1;
        vector<vector<int>> distance;
        distance.assign(N, vector<int>(N, 1e9));

        priority_queue<mars, vector<mars>, cmp> pq;
        pq.push(mars{ 0, 0, map[0][0] });

        distance[0][0] = map[0][0];

        while (!pq.empty())
        {
            mars m = pq.top();
            pq.pop();

            if (distance[m.x][m.y] < m.val)
            {
                continue;
            }

            for (int i = 0; i < 4; i++)
            {
                int nx = m.x + dir_x[i];
                int ny = m.y + dir_y[i];

                if (nx < 0 || ny < 0 || nx >= N || ny >= N)
                {
                    continue;
                }

                int cost = m.val + map[nx][ny];

                if (cost < distance[nx][ny])
                {
                    distance[nx][ny] = cost;
                    pq.push(mars{ nx, ny, cost });
                }
            }
        }

        answer = distance[N - 1][N - 1];

        return answer;
    }

    /*
    3
    5 5 4
    3 9 1
    3 2 7

    5
    3 7 2 0 1
    2 8 0 9 1
    1 2 1 8 1
    9 8 9 2 0
    3 6 5 1 5

    7
    9 0 5 1 1 5 3
    4 1 2 1 6 5 3
    0 7 6 1 6 8 5
    1 1 7 8 3 2 3
    9 4 0 7 6 4 1
    5 8 3 2 4 8 3
    7 4 8 4 8 3 4
    */

# 22.08.10(수)
