#  백준 - 도시 분할 계획

### 이 문제를 풀기 위한 과정
이 문제의 핵심 아이디어는 전체 그래프에서 2개의 최소 신장 트리를 만들어야 한다는 것이다.  
1. 크루스칼 알고리즘을 최소 신장 트리를 찾은 뒤에 최소 신장 트리를 구성하는 간선 중에서 가장 비용이 큰 간선을 제거한다.  
2. 최소 신장 트리를 찾은 뒤에 가장 큰 간선을 제거하면 답이 나온다.  

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    struct edge
    {
        int v1;
        int v2;
        int cost;
    };

    bool cmp(edge e1, edge e2)
    {
        if (e1.cost < e2.cost)
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    int solution(int N, vector<edge> vec);
    int find_parent(vector<int>& parent, int x);
    void union_parent(vector<int>& parent, int a, int b);

    int main(void)
    {
        int N, M;
        cin >> N >> M;

        vector<edge> vec;

        for (int i = 0; i < M; i++)
        {
            int A, B, C;
            cin >> A >> B >> C;

            vec.push_back(edge{ A, B, C });
        }

        int answer = solution(N, vec);

        cout << answer;
    }

    int solution(int N, vector<edge> vec)
    {
        int ans = 0;

        sort(vec.begin(), vec.end(), cmp);

        vector<int> parent;
        parent.assign(N + 1, 0);

        for (int i = 0; i < N + 1; i++)
        {
            parent[i] = i;
        }

        int last = 0;

        for (int i = 0; i < vec.size(); i++)
        {
            edge e = vec[i];

            if (find_parent(parent, e.v1) != find_parent(parent, e.v2))
            {
                union_parent(parent, e.v1, e.v2);
                ans = ans + e.cost;
                last = e.cost;
            }
        }

        return ans - last;

    }

    int find_parent(vector<int>& parent, int x)
    {
        if (parent[x] != x)
        {
            parent[x] = find_parent(parent, parent[x]);
        }
        return parent[x];
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

    /*
    7 12
    1 2 3
    1 3 2
    3 2 1
    2 5 2
    3 4 4
    7 3 6
    5 1 5
    1 6 2
    6 4 1
    6 5 3
    4 5 3
    6 7 4
    */

# 22.11.18(금)
* 