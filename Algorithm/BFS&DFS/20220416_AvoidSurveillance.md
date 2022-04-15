# 백준 - 감시 피하기(DFS)

### 이 문제를 풀기 위한 과정
N = 6 이므로장애물을 설치하는 시간복잡도는 36C3이다. 이는 10,000이하의 수이므로 모든 조합을 고려하여 완전 탐색을 수행해도 시간초과 없이 해결 할 수 있다.
따라서 모든 조합을 찾기 위해서 DFS 혹은 BFS를 이용해 장애물 3개 설치를 조합하는 함수를 작성하면 된다.
if else으로 한다면 백트래킹이 안된다.


CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    void DFS(int depth, int idx);
    bool watchTeacher();

    static int dir_x[] = { 0, -1, 0, 1 };
    static int dir_y[] = { -1, 0, 1, 0 };

    int N;
    vector<vector<string>> map;
    vector<pair<int, int>> teacher;
    string answer;
    bool b_find = false;

    int main()
    {
        cin >> N;

        map.assign(N, vector<string>(N, ""));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                cin >> map[i][j];

                if (map[i][j] == "T")
                {
                    teacher.push_back(make_pair(i, j));
                }
            }
        }

        DFS(0, 0);

        if (b_find == true)
            cout << "YES";
        else
            cout << "NO";
        

        return 0;
    }


    void DFS(int depth, int idx)
    {
        if (depth == 3)
        {
            if (!watchTeacher())
            {
                b_find = true;
            }
            
            return ;
        }

        for (int i = idx; i < map.size() * map.size(); i++)
        {
            int x = i / N;
            int y = i % N;

            if (map[x][y] == "X")
            {
                map[x][y] = "O";
                DFS(depth + 1, i + 1);
                if (b_find == true) return;
                map[x][y] = "X";
            }
        }

    }

    bool watchTeacher()
    {
        int new_x, new_y;

        for (pair<int,int> p : teacher)
        {
            for (int i = 0; i < 4; i++)
            {
                int new_x = p.first;
                int new_y = p.second;

                while (true)
                {
                    new_x = new_x + dir_x[i];
                    new_y = new_y + dir_y[i];

                    if (new_x < 0 || new_y < 0 || new_x >= N || new_y >= N) break;
                    if (map[new_x][new_y] == "O") break;
                    if (map[new_x][new_y] == "S") return true;
                }
            }
        }
        return false;
    }


# 22.04.13(금)
* depth가 가득 찼을 때 return 을 작성을 안해 시간초과가 나왔다. 이 실수로 인해 거의 하루를 날려버렸다....
앞으로 주의해서 코드를 작성하자