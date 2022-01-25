# 백준 - 경쟁적 전염

### 이 문제를 풀기 위한 과정
이 문제는 간단하게 BFS으로 문제 해결을 할 수 있다. 다만, 주의점으로 바이러스가 낮은 번호부터 증식한다는 점이다.
초기에 정렬을 하여 원소를 빼내어 사용하면 된다.

현재 난 vector 하나만을 사용하여 정렬을 매 시간초 마다 정렬을 하여서 문제를 해결하여 140ms 정도의 시간이 나왔다.
하지만 다른 사람들의 답안을 보면 vector를 한번만 정렬하여 queue에 삽입한다.
그 후 queue에서 원소를 push, pop하여 4ms의 시간이 나오는 것을 볼 수 있었다. (정렬이 한번밖에 수행되지 않았다)

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>
    #include <queue>

    using namespace std;

    int solution();
    void bfs();

    class Virus {
    public:
        int x;
        int y;
        int value;
    };


    bool cmp(Virus v1, Virus v2)
    {
        return v1.value < v2.value;
    }

    int N, K;
    int S, X, Y;
    vector<vector<int>> map;
    vector<Virus> vec;

    int dir_x[4] = { 0, -1, 0, 1 };
    int dir_y[4] = { -1, 0, 1, 0 };

    int main(void)
    {
        int answer;

        cin >> N >> K;
        map.assign(N, vector<int>(N,0));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                cin >> map[i][j];

                if (map[i][j] != 0)
                {
                    Virus virus = Virus();
                    virus.x = i;
                    virus.y = j;
                    virus.value = map[i][j];
                    vec.push_back(virus);
                }
                
            }
        }

        cin >> S >> X >> Y;

        answer = solution();
        
        cout << answer;
    }

    int solution() 
    {
        for (int s = 0; s < S; s++)
        {
            sort(vec.begin(), vec.end(), cmp);
            bfs();
        }

        return map[X - 1][Y - 1];
    }

    void bfs()
    {
        int new_x, new_y;
        int len = vec.size();

        for(int k = 0; k<len; k++)
        {
            Virus virus = vec.front();
            vec.erase(vec.begin() + 0);

            for (int i = 0; i < 4; i++)
            {
                new_x = virus.x + dir_x[i];
                new_y = virus.y + dir_y[i];

                if (new_x >= 0 && new_y >= 0 && new_x < N && new_y < N)
                {
                    if (map[new_x][new_y] == 0)
                    {
                        map[new_x][new_y] = virus.value;
                        Virus add_virus = Virus();
                        add_virus.x = new_x;
                        add_virus.y = new_y;
                        add_virus.value = virus.value;
                        vec.push_back(add_virus);
                    }
                }
            }
        }
    }




# 22.01.25화)
* 기초적인 BFS 문제였지만 다른 사람의 풀이와 나의 풀이의 시간 차이가 어마어마했다.
* 좀 더 효율적인 코딩을 짤 수 있는 실력이 되어야겠다....