# 백준 - 연산자 끼워넣기

### 이 문제를 풀기 위한 과정
이 문제는 완전탐색, DFS 혹은 BFS으로 문제를 풀 수 있다. 현재 이 페이지에서는 순열을 이용하여 완전탐색으로 문제를 해결하였다.
중복 순열으로도 풀어도 되지만, 중복x 순열으로 풀기 위해 사칙연산을 입력받을때마다 vector에 하나씩 넣어서 나중에 하나씩 빼서 사용하였다.

CODE1

    #include <stdio.h>
    #include <iostream>
    #include <vector>
    #include <string>
    #include <algorithm>

    using namespace std;

    int N;
    vector<int> A;
    vector<string> opt;
    vector<string> permu;
    vector<bool> check_opt;


    vector<int> answer;

    void solution(int depth);
    int changeToInt(int n, string operation, int m);

    int main()
    {
        cin >> N;
        
        int num;
        for (int i = 0; i < N; i++)
        {
            cin >> num;
            A.push_back(num);
        }

        check_opt.assign(N - 1, false);

        for (int i = 0; i < 4; i++)
        {
            cin >> num;
            for (int j = 0; j < num; j++)
            {
                switch (i) {
                    case 0: 
                        opt.push_back("+");
                        break;
                    case 1:
                        opt.push_back("-");
                        break;
                    case 2:
                        opt.push_back("*");
                        break;
                    case 3:
                        opt.push_back("/");
                        break;
                    default:
                        break;
                }
            }
        }
        
        solution(0);

        int i_max;
        int i_min;
        i_max = *max_element(answer.begin(), answer.end());
        i_min = *min_element(answer.begin(), answer.end());

        cout << i_max << endl;
        cout << i_min << endl;
    }

    void solution(int depth)
    {
        if (depth == N - 1)
        {
            int result = A[0];

            for (int i = 0; i < N-1; i++) {
                result = changeToInt(result, permu[i], A[i + 1]);
            }

            answer.push_back(result);
            return;
        }

        for (int i = 0; i < N - 1; i++)
        {
            if (!check_opt[i]) {
                permu.push_back(opt[i]);
                check_opt[i] = true;
                solution(depth + 1);
                check_opt[i] = false;
                permu.erase(permu.end()-1, permu.end());
            }
        }

    }

    int changeToInt(int n, string operation, int m)
    {
        int i_return = 0;

        if (operation.compare("+") == 0)
        {
            i_return = n + m;
        }
        else if (operation.compare("-") == 0)
        {
            i_return = n - m;
        }
        else if (operation.compare("*") == 0)
        {
            i_return = n * m;
        }
        else if (operation.compare("/") == 0)
        {
            i_return = n / m;
        }

        return i_return;
    }



# 22.01.28(금)
* 다음에는 이 문제를 DFS으로도 풀수 있다고 하는데 풀어봐야겠다.