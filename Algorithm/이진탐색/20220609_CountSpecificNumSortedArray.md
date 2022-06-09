# 동빈나 책 - 정렬된 배열에서 특정 수의 개수 구하기

### 이 문제를 풀기 위한 과정
시간 복잡도 logN으로 동작하는 알고리즘을 요구하고 있다. 따라서 일반적인 선형탐색으로는 문제를 해결 할 수 없다. 

1. X가 처음 등장하는 인덱스와 X가 마지막으로 등장하는 인덱스를 가각 계산 한 뒤에
2. 인덱스의 차이를 계산하여 문제를 해결할 수 있다.

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    int solution(int X, vector<int> vec);

    int main(void)
    {
        int N, X;
        vector<int> vec;

        cin >> N >> X;

        int num = 0;

        for (int i = 0; i < N; i++)
        {
            cin >> num;
            vec.push_back(num);
        }

        int answer = solution(X, vec);

        cout << answer;
    }

    int solution(int X, vector<int> vec)
    {
        int answer = 0;

        sort(vec.begin(), vec.end());

        answer = upper_bound(vec.begin(), vec.end(), X) - lower_bound(vec.begin(), vec.end(), X);


        if (answer == 0)
            answer = -1;

        return answer;

    }

# 22.06.09(목)
* upper_bound, lower_bound 복습!