#  이코테 - 여행 계획

### 이 문제를 풀기 위한 과정
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20221122_TravelPlan1.PNG)

이 문제는 서로서 집합 알고리즘을 이용하여, 그래프에서 노드 간의 연결성을 파악해 해결할 수 있다.  
여행 계획에 해당하는 모든 노드가 같은 집합에 속하기만 하면 가능한 여행 경로이다.  
따라서 두 노드 사이에 도로가 존재하는 경우에는 union(합집합) 연산을 이용해서, 서로 연결된 두 노드를 같은 집합에 속하도록 만든다.  
결과적으로 입력으로 들어온 "여행 계획"에 포함되는 모든 노드가 모두 같은 집합에 속하는지를 체크하여 출력하면 정답 판정을 받을 수 있다.  



CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    string solution(int N, vector<vector<int>> graph, vector<int> route);

    void union_parent(vector<int>& parent, int a, int b);
    int find_parent(vector<int>& parent, int x);

    int main(void)
    {
        int N, M;
        cin >> N >> M;

        vector<vector<int>> graph;
        graph.assign(N + 1, vector<int>(0, 0));

        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= N; j++)
            {
                int num;
                cin >> num;

                if (num == 1)
                {
                    graph[i].push_back(j);
                }
            }
        }

        vector<int> route;
        route.assign(M, 0);
        for (int i = 0; i < M; i++)
        {
            int num;
            cin >> num;

            route[i] = num;
        }

        string answer = solution(N, graph, route);

        cout << answer;
    }

    string solution(int N, vector<vector<int>> graph, vector<int> route)
    {
        string ans = "YES";

        vector<int> parent;
        parent.assign(N + 1, 0);

        for (int i = 1; i <= N; i++)
        {
            parent[i] = i;
        }

        for (int i = 1; i <= N; i++)
        {
            for (int j = 0; j < graph[i].size(); j++)
            {
                union_parent(parent, i, graph[i][j]);
            }
        }

        int root = find_parent(parent, route[0]);

        for (int i = 1; i < route.size(); i++)
        {
            int x = route[i];

            if (root != find_parent(parent, x))
            {
                ans = "NO";
            }
        }


        return ans;
    }

    void union_parent(vector<int>& parent, int a, int b)
    {
        a = find_parent(parent, a);
        b = find_parent(parent, b);

        if (a < b)
        {
            parent[b] = a;
        }
        else
        {
            parent[a] = b;
        }
    }

    int find_parent(vector<int>& parent, int x)
    {
        if (parent[x] != x)
        {
            parent[x] = find_parent(parent, parent[x]);
        }

        return parent[x];
    }

    /*
    5 4
    0 1 0 1 1
    1 0 1 1 0
    0 1 0 0 0
    1 1 0 0 0
    1 0 0 0 0
    2 3 4 3
    */

# 22.11.22(화)
* 이 문제의 핵심은 여행 계획에 해당하는 모든 노드가 같은 집합에 포함되면 가능한 여행 경로이라는 것이다.  