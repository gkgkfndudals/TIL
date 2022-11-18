#  이코테 - 팀 결성

### 이 문제를 풀기 위한 과정
전형적인 서로소 집합 알고리즘 문제이다.  
N과 M의 범위가 모두 최대 100,000이다. 따라서 경로 압축 방식의 서로서 집합 자료구조를 이용하여 시간 복잡도를 개선해야 한다.  

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    struct team
    {
        int oper;
        int v1;
        int v2;
    };

    vector<string> solution(int N, vector<team> vec);
    int find_parent(vector<int>& parent, int x);
    void union_parent(vector<int>& parent, int a, int b);

    int main(void)
    {
        int N, M;
        cin >> N >> M;

        vector<team> vec;
        for (int i = 0; i < M; i++)
        {
            int oper, v1, v2;
            cin >> oper >> v1 >> v2;

            vec.push_back(team{ oper, v1, v2 });
        }

        vector<string> answer = solution(N, vec);

        for (int i = 0; i < answer.size(); i++)
        {
            cout << answer[i] << endl;
        }
    }

    vector<string> solution(int N, vector<team> vec)
    {
        vector<string> ans;
        vector<int> parent;
        parent.assign(N + 1, 0);

        for (int i = 0; i < N + 1; i++)
        {
            parent[i] = i;
        }

        for (int i = 0; i < vec.size(); i++)
        {
            team t = vec[i];
            if (t.oper == 0)
            {
                union_parent(parent, t.v1, t.v2);
            }
            else
            {
                if (find_parent(parent, t.v1) == find_parent(parent, t.v2))
                {
                    ans.push_back("YES");
                }
                else
                {
                    ans.push_back("NO");
                }
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
    7 8
    0 1 3
    1 1 7
    0 7 6
    1 7 1
    0 3 7
    0 4 2
    0 1 1
    1 1 1
    */

# 22.11.18(금)
* 