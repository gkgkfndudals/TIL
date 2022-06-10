# 백준 - 공유기 설치

### 이 문제를 풀기 위한 과정
이 문제는 '가장 인접한 두 공유기 사이의 거리'의 최댓값을 탐색해야 하는 문제이다.  
각 집의 좌표가 최대 10억이므로 이진 탐색을 이용하면 문제를 해결할 수 있다.  
따라서 이진 탐색으로 '가장 인접한 두 공유기 사이의 거리'를 조절해가며, 매 순간 실제로 공유기를 설치하여 C보다 많은 개수로 공유기를 설치할 수 있는지 체크하여 문제를 해결할 수 있다.

1. 공유기 설치 좌표들을 오름차순으로 정렬합니다. (이분 탐색의 기본 조건)
2. 공유기를 가장 공평하게 설치할 수 있는 간격(mid)을 구합니다.
3. 첫 번째 집에 공유기를 설치한 뒤, 첫 번째 집에서 나머지 집들 간의 간격을 확인하며, mid 이상으로 떨어져 있는 집을 탐색합니다.
4. 첫 번째 집으로부터 mid 이상 떨어진 집을 찾은 경우, 해당 집에 공유기를 설치한 뒤, 해당 집 기준으로 다시 mid 만큼 떨어져있는 집을 탐색합니다.
5. 모든 집을 탐색했다면, 공유기를 공평하게 설치할 수 있는 간격을 이분법을 사용해 갱신합니다.
    * 현재까지 설치한 공유기 개수가 아직 C개 이하라면, 기존 간격이 너무 크다는 의미이므로, 기존 간격보다 더 작은 간격으로 갱신합니다.
    * 현재까지 설치한 공유기 개수가 C개 이상이라면, 기존 간격이 너무 작다는 의미이므로, 기존 간격보다 더 큰 간격으로 갱신합니다.
6. 이분법을 사용해 모든 간격들을 탐색할 때까지 3번~5번 과정을 반복합니다.
7. 탐색된 최대 간격을 반환합니다.

CODE1

    #include <iostream>
    #include <vector>
    #include <algorithm>
    using namespace std;

    int solution(int N, int C, vector<int> vec);

    int main(void)
    {
        int N, C;

        cin >> N >> C;

        vector<int> vec;
        int num = 0;

        for (int i = 0; i < N; i++)
        {
            cin >> num;
            vec.push_back(num);
        }

        int answer = solution(N, C, vec);

        cout << answer;
    }

    int solution(int N, int C, vector<int> vec)
    {
        int answer = -1;

        sort(vec.begin(), vec.end());

        int left = 0;
        int right = vec[N-1] - vec[0];
        int mid = 0;

        while (left <= right)
        {
            int cnt = 1;
            mid = (left + right) / 2;
            int pre_idx = 0;

            for (int i = 1; i < N; i++)
            {
                int dist = vec[i] - vec[pre_idx];

                if (mid <= dist)
                {
                    pre_idx = i;
                    cnt++;
                }
            }

            if (cnt >= C)
            {
                left = mid + 1;
                answer = max(answer, mid);
            }
            else
            {
                right = mid - 1;
            }
        }

        return answer;
    }

# 22.06.10(금)
* 처음에는 if(cnt == C)라고 코드를 작성하였는데 틀렸다고 나왔다. 하지만 곰곰히 생각을 해보니 C개보다 많이 설치할 수 있다는 것은 곧 C개도 설치할 수 있음을 의미한다는 것을 볼 수 있습니다.  
이진탐색 알고리즘 연습하기에 좋은 문제라고 생각한다. 나중에 다시 한번 이 문제를 풀어보는 것이 좋을 것 같다.