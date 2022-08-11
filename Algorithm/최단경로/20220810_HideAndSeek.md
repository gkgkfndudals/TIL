#  이코테 - 숨바꼭질

### 이 문제를 풀기 위한 과정
이 문제는 다익스트라 알고리즘을 이용하여 1번 노드(헛간)로부터 다른 모든 노드로의 최단 거리를 계산한뒤, 가장 최단 거리가 긴 노드를 찾는 문제이다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220811_HideAndSeek1.PNG)

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220811_HideAndSeek2.PNG)

따라서 최단 거리가 가장 긴 노드까지의 최단 거리는 '2'라는 것을 알 수 있다.  
최단 거리가 2인 노드가 3개인 것을 확인 할 수 있다.  
문제에서 최단 거리가 같은 헛간이 여러 개이면 가장 작은 노드 번호인 4번 노드를 출력한다.  

CODE1

    #include <iostream>
    #include <vector>
    #include <queue>

    using namespace std;

    vector<int> solution(int N, vector<vector<pair<int, int>>> graph);

    struct cmp
    {
        bool operator()(pair<int, int>& a, pair<int, int>& b)
        {
            return a.second < b.second;
        }
    };

    int main(void)
    {
        int N, M;
        cin >> N >> M;

        vector<vector< pair<int, int> >> graph;
        graph.assign(N + 1, vector<pair<int, int>>());

        for (int i = 0; i < M; i++)
        {
            int a, b;
            cin >> a >> b;
            graph[a].push_back(make_pair(b, 1));
            graph[b].push_back(make_pair(a, 1));
        }

        vector<int> answer = solution(N, graph);

        for (int i = 0; i < answer.size(); i++)
        {
            cout << answer[i] << " ";
        }

    }

    vector<int> solution(int N, vector<vector<pair<int, int>>> graph)
    {
        vector<int> answer;
        vector<int> distance;
        distance.assign(N + 1, 1e9);
        distance[1] = 0;

        priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> pq;

        pq.push(make_pair(1, 0));

        while (!pq.empty())
        {
            int current = pq.top().first;
            int cost = pq.top().second;
            pq.pop();

            if (distance[current] < cost)
            {
                continue;
            }

            for (int i = 0; i < graph[current].size(); i++)
            {
                int next_node = graph[current][i].first;
                int nextDistance = graph[current][i].second + cost;

                if (nextDistance < distance[next_node])
                {
                    distance[next_node] = nextDistance;
                    pq.push(make_pair(next_node, nextDistance));
                }
            }
        }

        int max_distance = -1;
        int min_node = 1e9;
        int cnt = 0;

        for (int i = 1; i < distance.size(); i++)
        {
            max_distance = max(max_distance, distance[i]);
        }

        for (int i = 0; i < distance.size(); i++)
        {
            if (max_distance == distance[i])
            {
                min_node = min(min_node, i);
                cnt++;
            }
        }

        answer.push_back(min_node);
        answer.push_back(max_distance);
        answer.push_back(cnt);

        return answer;
    }

    /*
    6 7
    3 6
    4 3
    3 2
    1 3
    1 2
    2 4
    5 2
    */

# 22.08.11(목)
* 문제에서의 거리가 1이기 때문에 BFS를 이용하여 최단 거리를 계산 할 수 있다. BFS로도 한번 꼭 풀어보도록 하자.  