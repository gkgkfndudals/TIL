# 동빈나 책 - 고정점 찾기

### 이 문제를 풀기 위한 과정
이진 탐색을 수행해서 고정점을 찾는게 핵심이다.

1. 중간점이 가리키는 위치의 값보다 중간점이 작은 경우(vec[mid] > mid)에는 start를 갱신
2. 중간점이 가리키는 위치의 값보다 중간점이 큰 경우(vec[mid] < mid)에는 end를 갱신

CODE1

    #include <iostream>
    #include <vector>
    using namespace std;

    int solution(int N, vector<int> vec);

    int main(void)
    {
        int N;
        vector<int> vec;

        cin >> N;

        int num;

        for (int i = 0; i < N; i++)
        {
            cin >> num;
            vec.push_back(num);
        }

        int answer = solution(N, vec);

        cout << answer;
    }

    int solution(int N, vector<int> vec)
    {
        int answer = -1;

        int start = 0;
        int end = N - 1;

        while (start <= end)
        {
            int mid = (start + end) / 2;
            int num = vec[mid];

            if (num > mid)
            {
                end = mid - 1;
            }
            else if (num < mid)
            {
                start = mid + 1;
            }
            else
            {
                answer = mid;
                break;
            }
        }

        return answer;
    }

# 22.06.09(목)
* 전형적인 이진 탐색의 기초이다. 외워두도록 하자.