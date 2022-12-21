#  이코테 - 행성 터널

### 이 문제를 풀기 위한 과정
이 문제는 N - 1개의 터널을 설치해서 모든 행성이 연결되도록 요구하므로, 최소 신장 트리 문제이다.  
간선의 개수는 N(N-1)/2개가 될 것이다. N이 최대 100,000이므로 크루스칼 알고리즘 O(ElogE)을 사용한다고 해도 시간초과가 나올 수도 있다.  

터널의 비용이 min(|Xa-Xb|, |Ya-Yb|, |Za-Zb|)라고 정의 되어 있다. 이러한 점을 이용하면 간선의 개수를 줄일 수 있다.  
x, y, z 축을 기준으로 각각 정렬을 수행한다. 그리고 각 축에서의 거리를 계산하여 edge에 넣어주고 다시 정렬한다. 그러면 N-1개의 간선만 고려하여 문제를 해결하면 된다.  
결과적으로 x, y, z 축에 대하여 정렬 이후에 각각 N - 1 개의 간선만 고려해도 최적의 솔루션을 찾을 수 있다.  

**예시1)**  
(11, -15, -15), (14, -5, -15), (-1, -1, -5), (10, -4, -1), (19, -4, 19)의 좌표를 가정하면  
이때 x 축만 고려해서 정렬을 수행하면 -1, 10, 11, 14, 19가 된다. 그리고 x축에서의 거리는 차례대로 11, 1, 3, 5가 된다.  
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20221221_PlanetTunnel.PNG)

**예시2)**  
- 각 행성들의 X,Y,Z 좌표를 별도로 벡터에 담아두고 오름차순 정렬해 놓는다.
- X 좌표를 우선 예로 들면, 행성 A. B, C, D 의 X좌표가 각각 11, 3, 2, 8 이었을 경우 오름차순 정렬하면 2, 3, 8, 11 이며, 각각 C, B, D, A 순이다.
- 따라서 행성 C-B, B-D, D-A 로 연결될 때 각각의 X좌표 차이(3-2, 8-3, 11-8)가 행성들 간 X좌표 차이의 최솟값이 된다.
- 즉, 행성 C는 B와 연결될 때 X좌표 차이가 가장 작으며, 행성 B는 행성 D와 연결될 때 X좌표 차이가 가장 작다.
- Y, Z 좌표에도 위와 똑같은 방법을 적용한다. 그리고 구해진 X, Y, Z 좌표 차이의 최솟값들 모음을 가지고 크루스칼 알고리즘을 진행한다.

고려한 총 간선의 개수는 3 X (N - 1)개가 되고, 이를 크루스칼 알고리즘을 수행하면 제한 시간안에 해결 가능하다.
 
CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>
    #include <cstdlib>

    using namespace std;

    struct planet
    {
        int x;
        int y;
        int z;
    };

    struct edge
    {
        int v1;
        int v2;
        int cost;
    };

    bool cmp(pair<int, int>& a, pair<int, int>& b)
    {
        return a.first < b.first;
    }

    bool edgeCmp(edge &e1, edge &e2)
    {
        return e1.cost < e2.cost;
    }

    int solution(int N, vector<planet> vec);
    int find_parent(vector<int>& parent, int x);
    void union_parent(vector<int>& parent, int a, int b);

    int main(void)
    {
        int N;
        cin >> N;
        
        vector<planet> vec;

        for(int i = 0; i < N; i++)
        {
            int x, y, z;
            cin >> x >> y >> z;
            vec.push_back(planet{x, y, z});
        }

        int answer = solution(N, vec);
        
        cout << answer;
    }

    int solution(int N, vector<planet> vec)
    {
        int ans = 0;

        vector<pair<int, int>> v_x, v_y, v_z;

        for(int i = 0 ; i < N; i++)
        {
            v_x.push_back(make_pair(vec[i].x, i));
            v_y.push_back(make_pair(vec[i].y, i));
            v_z.push_back(make_pair(vec[i].z, i));
        }

        sort(v_x.begin(), v_x.end(), cmp);
        sort(v_y.begin(), v_y.end(), cmp);
        sort(v_z.begin(), v_z.end(), cmp);
        
        vector<edge> e;

        for(int i = 1; i < N; i++)
        {
            int v1, v2, cost;
            v1 = v_x[i-1].second;
            v2 = v_x[i].second;
            cost = abs(v_x[i-1].first - v_x[i].first);
            e.push_back(edge{v1, v2, cost});

            v1 = v_y[i-1].second;
            v2 = v_y[i].second;
            cost = abs(v_y[i-1].first - v_y[i].first);
            e.push_back(edge{v1, v2, cost});

            v1 = v_z[i-1].second;
            v2 = v_z[i].second;
            cost = abs(v_z[i-1].first - v_z[i].first);
            e.push_back(edge{v1, v2, cost});
        }

        sort(e.begin(), e.end(), edgeCmp);

        vector<int> parent;
        parent.assign(N, 0);
        for(int i = 0; i < N; i++)
        {
            parent[i] = i;
        }

        for(int i = 0; i < e.size(); i++)
        {
            if(find_parent(parent, e[i].v1) != find_parent(parent, e[i].v2))
            {
                union_parent(parent, e[i].v1, e[i].v2);
                ans += e[i].cost;
            }
        }
        
        return ans;
    }

    int find_parent(vector<int>& parent, int x)
    {
        if(parent[x] != x)
        {
            parent[x] = find_parent(parent, parent[x]);
        }

        return parent[x];
    }

    void union_parent(vector<int>& parent, int a, int b)
    {
        a = find_parent(parent, a);
        b = find_parent(parent, b);

        if(a < b)
        {
            parent[b] = a;
        }
        else
        {
            parent[a] = b;
        }
    }

    /*
    5
    11 -15 -15
    14 -5 -15
    -1 -1 -5
    10 -4 -1
    19 -4 19
    */

# 22.12.21(수)
* 크루스칼 알고리즘 문제중에서 처음으로 플래티넘 문제를 풀어보았다.
* 행성들 간의 X, Y, Z 좌표값 차이 중 가장 작은 값들이 간선 가중치 후보가 될 수 있는 것을 x, y, z 축들을 정렬한 후에 절대값을 계산한 후 edge 구조체를 만드는 것이 신기하였다.
* 이러한 방법을 몰라 결국 해답을 보고 문제를 풀었는데, 다음에 비슷한 문제가 나온다면 이 부분을 꼭 기억해서 풀자