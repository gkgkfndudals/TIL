# 프로그래머스 - 기둥과 보 설치

### 이 문제를 풀기 위한 과정
이 문제는 전형적인 시뮬레이션 문제이다. 문제에서 제시한 구체적인 처리 과정을 프로그램상에서 차례대로 수행하여 결과를 도출하는게 핵심
1. 요규사항을 확인해보면, 전체 명령의 개수는 총 1000개 이하이고, 시간 제한은 5초이다.
2. 그러므로 O(M^3)으로 문제를 해결하여도 된다.
3. 설치 및 삭제 연산을 요구할 때마다 '전체 구조물을 확인하며' 규칙을 확인한다.
4. 매번 check(int x, int y, int a) 함수를 호출하여 전체 map을 돌면서 구조물이 정상인지 체크하고, 정상이 아니라면 연산을 되돌려 준다.
5. check의 각 조건은 문제에서 다 주어져있다. 잘 읽어보고 이해한다면 충분히 조건을 코드화 할 수 있다.

CODE1

    #include <iostream>
    #include <string>
    #include <vector>
    #include <algorithm>

    using namespace std;
    vector<vector<vector<int>>> map;
    vector<vector<int>> solution(int n, vector<vector<int>> build_frame);

    bool check(int x, int y, int a) {
        if (a == 0) {
            if (y==0 || (y - 1 >= 0 && map[0][x][y - 1])
                || map[1][x][y] || (x - 1 >= 0 && map[1][x - 1][y]))
                return true;
        }
        else {
            if ((y - 1 >= 0 && map[0][x][y - 1]) || (y - 1 >= 0 && map[0][x + 1][y - 1])
                || (x - 1 >= 0 && map[1][x - 1][y] && map[1][x + 1][y]))
                return true;
        }
        return false;
    }


    void main(void)
    {
        int num = 0;
        int n = 5;
        vector<vector<int>> build_frame;
        vector<int> v;
        for (int i = 0; i < 8; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                cin >> num;
                v.push_back(num);
            }
            build_frame.push_back(v);
            v.clear();
        }

        solution(n, build_frame);
    }

    vector<vector<int>> solution(int n, vector<vector<int>> build_frame) {
        vector<vector<int>> answer;
        
        map.assign(2, vector<vector<int>>(n + 1, vector<int>(n + 1)));

        for (int i = 0; i < build_frame.size(); i++)
        {
            vector<int> operation = build_frame[i];
            int x = operation[0];
            int y = operation[1];
            int a = operation[2];
            int b = operation[3];
            
            if (b == 1)
            {
                if (check(x, y, a))
                    map[a][x][y] = 1;
            }
            else
            {
                map[a][x][y] = 0;
                for (int i = 0; i < n; i++) 
                {
                    for (int j = 0; j < n; j++) 
                    {
                        for (int k = 0; k < 2; k++) 
                        {
                            if (map[k][i][j] == 1 && !check(i, j, k))
                                map[a][x][y] = 1;
                        }
                    }
                }
            }
        }

        for (int i = 0; i <= n; i++)
        {
            for (int j = 0; j <= n; j++)
            {
                for (int k = 0; k < 2; k++)
                {
                    if (map[k][i][j] == 1)
                        answer.push_back({ i,j,k });
                }
            }
        }

        return answer;
    }




# 21.12.21(화)
* 이 문제를 푸는데 7시간이나 걸렸다....
* 문제에서 n의 입력 값이 -1 작은 값으로 주어진 것도 모르고 하루종일 index 오류에 시달렸다....
* 문제 자체도 너무 빡구현이여서 조건을 코딩으로 적고 구현하는데 시간이 많이 걸렸다.
* 정말 다시 풀기 싫어지는 문제이다. 하루종일 스트레스를 받는 하루가 되었다.