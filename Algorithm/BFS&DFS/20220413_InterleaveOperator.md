# 백준 - 연산자 끼워넣기(DFS)

### 이 문제를 풀기 위한 과정
이 문제는 완전탐색(중복 순열), DFS 혹은 BFS으로 문제를 풀 수 있다. 현재 코드는 DFS으로 문제를 풀었다.
depth가 차면 max, min 을 갱신 시켜주고 리턴을 해준다. 그리고 각각 연산에 대해서 if으로 해줘야된다.
if else으로 한다면 백트래킹이 안된다.


CODE1

    #include <iostream>
    #include <vector>
    #include <climits>
    #include <algorithm>

    using namespace std;

    void DFS(int plus, int sub, int mul, int div, int depth, int num);

    int N;
    vector<int> A;
    vector<int> opt;
    int i_max = INT_MIN;
    int i_min = INT_MAX;

    int main(void) {
        cin >> N;

        A.assign(N, 0);
        opt.assign(4, 0);
        for (int i = 0; i < N; i++)
        {
            cin >> A[i];
        }

        for (int i = 0; i < 4; i++)
        {
            cin >> opt[i];
        }

        DFS(opt[0], opt[1], opt[2], opt[3], 0, A[0]);

        cout << i_max << endl;
        cout << i_min << endl;

        return 0;
    }

    void DFS(int plus, int sub, int mul, int div, int depth, int num)
    {
        if (N - 1 == depth)
        {
            i_max = max(i_max, num);
            i_min = min(i_min, num);
            cout << endl;
            return;
        }

        if (plus > 0)
        {
            DFS(plus - 1, sub, mul, div, depth + 1, num + A[depth + 1]);
        }
        if (sub > 0)
        {
            DFS(plus, sub - 1, mul, div, depth + 1, num - A[depth + 1]);
        }
        if (mul > 0)
        {
            DFS(plus, sub, mul - 1, div, depth + 1, num * A[depth + 1]);
        }
        if (div > 0)
        {
            DFS(plus, sub, mul, div - 1, depth + 1, num / A[depth + 1]);
        }
    }


# 22.04.13(금)
* 확실히 아직 백트래킹 문제에서 많이 막히는게 느껴진다....