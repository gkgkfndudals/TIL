#  이코테 - 서로서 집합을 활용한 사이클 판별

### 이 문제를 풀기 위한 과정
1. 각 간선을 확인하며 두 노드의 루트 노드를 확인한다.
    - 루트 노드가 서로 다르다면 두 노드에 대하여 union 연산을 수행한다.
    - 루트 노드가 서로 같다면 사이클이 발생한 것이다.
2. 그래프에 포함되어 있는 모든 간선에 대하여 1번 과정을 반복한다.

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int find_parent(vector<int>& parent, int num);
    void union_parent(vector<int>& parent, int a, int b);

    bool b_cycle = false;

    int main(void)
    {
        int v, e;
        int a, b;

        cin >> v >> e;

        vector<int> parent;
        parent.assign(v + 1, 0);
        for (int i = 1; i < v + 1; i++)
        {
            parent[i] = i;
        }
        
        for (int i = 0; i < e; i++)
        {
            cin >> a >> b;

            if (find_parent(parent, a) == find_parent(parent, b))
            {
                b_cycle = true;
                break;
            }
            else
            {
                union_parent(parent, a, b);
            }
        }

        if (b_cycle == true)
        {
            cout << "사이클이 발생하였습니다." << endl;
        }
        else
        {
            cout << "사이클이 발생하지 않았습니다." << endl;
        }

        for (int i = 1; i < v + 1; i++)
        {
            cout << find_parent(parent, i) << " ";
        }
    }

    int find_parent(vector<int>& parent, int num)
    {
        if (parent[num] != num)
        {
            parent[num] = find_parent(parent, parent[num]);
        }
        return parent[num];
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
    6 4
    1 4
    2 3
    2 4
    5 6
    */

# 22.10.14(금)
* 서로서 집합 union_find 문제이다.
* 사이클이 있는지 없는지는 무방향 그래프일때 확인한다.
* find_parent 에서 parent[num]을 업데이트 해주는, 경로 압축 방법을 적용한 부분을 외워두도록하자.