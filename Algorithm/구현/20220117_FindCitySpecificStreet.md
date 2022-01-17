# 백준 - 특정 거리의 도시 찾기

### 이 문제를 풀기 위한 과정
그래프에서 모든 간선의 비용이 동일할 때는 BFS을 이용하여 최단 거리를 찾을 수 있다.
문제의 조건을 살펴보면 노드의 개수 N은 최대 300,000개이며 간선의 개수 M은 최대 1,000,000개이다.
시간 복잡도 O(N+M)으로 동작
모든 도시까지의 최단 거리를 계산한 뒤에, 최단 거리가 K인 경우에 해당 도시의 번호를 출력한다.

1. 특정한 도시 x를 큐에 넣는다.
2. 큐에서 현재 도시를 pop하여 다음 node를 찾은 후, 처음으로 간 도시이면 (dist[nextNode] == -1) 그 도시의 거리를 업데이트 해준다.
3. 마지막으로 queue에 push 해주고, 반복문을 반복한다.

CODE1

    #include <iostream>
    #include <vector>
    #include <queue>
    #include <algorithm>

    using namespace std;

    vector<int> solution(vector<vector<int>> v, int K, int X, int N);

    int main(void)
    {
        vector<int> answer;
        vector<int> solReturn;
        int N, M, K, X;
        int A, B;
        vector<vector<int>> v;
        

        cin >> N >> M >> K >> X;
        
        v.assign(N+1, vector<int>(0));

        for (int i = 0; i < M; i++)
        {
            cin >> A >> B;
            v[A].push_back(B);
        }

        solReturn = solution(v, K, X, N);

        for (int i = 0; i < solReturn.size(); i++)
        {
            if (solReturn[i] == K)
            {
                answer.push_back(i);
            }
        }

        sort(answer.begin(), answer.end());

        if (answer.size() == 0)
        {
            cout << -1 << endl;
        }
        else
        {
            for (int i = 0; i < answer.size(); i++)
            {
                cout << answer[i] << endl;
            }
        }
            
        

        return 0;
    }

    vector<int> solution(vector<vector<int>> v, int K, int X, int N)
    {
        vector<int> dist;
        dist.assign(N+1, -1);
        dist[X] = 0;

        queue<int> q;
        q.push(X);
        
        while (!q.empty())
        {
            int now = q.front();
            q.pop();

            for (int i = 0; i < v[now].size(); i++)
            {
                int nextNode = v[now][i];

                if (dist[nextNode] == -1)
                {
                    dist[nextNode] = dist[now] + 1;
                    q.push(nextNode);
                }
            }
        }

        return dist;
    }



# 22.01.17(월)
* 옛날에 풀어본 문제인데도 어떻게 풀어야 될지 감이 안잡혀 조금 시간이 걸렸다. dist 벡터 이용하는 것 이라든가.....
* 모든 간선의 비용이 동일할 때는 BFS을 이용하는게 핵심이므로 기억하도록 하자