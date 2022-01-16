# 백준 - 치킨 배달

### 이 문제를 풀기 위한 과정
이 문제는 weak, dist 리스트의 길이가 매우 작으므로 완전탐색으로 접근해 볼 수 있다.
원형으로 나열 된 데이터를 처리하는 경우에는, 길이를 2배로 늘려서 '원형'을 일자 형태로 만들어 작업을 해주는게 좋다.
n= 12 이고 weak = [1, 5, 6, 10] 일때 weak = [1, 5, 6, 10, 13, 17, 18, 22]으로 만든다.
그리고 dist 배열의 모든 순열에 대해서 weak 배열의 모든 구간을 탐색하면 모든 경우의 수를 구할 수 있다.

1. 원형에 대한 weak 배열 가공
2. 순열 계산을 위한 dist를 정렬 해준다.
3. dist 순열마다 외벽검사를 해준다. 모든 지점 방문 완료 시 min값을 구한다 -> 순열 - 외벽 지점 - 친구(dist) 3중 반복문을 돈다.
4. 다음 검사 시작 지점 구하기 -> 마지막에 방문한 지점보다 큰 weak지점 중 가장 작은 지점을 구해야되기 때문에 upper_bound를 사용

CODE1

    #include <string>
    #include <vector>
    #include <algorithm>
    #include <iostream>

    using namespace std;

    int solution(int n, vector<int> weak, vector<int> dist);

    int solution(int n, vector<int> weak, vector<int> dist) {
        int answer = 0;

        int length = weak.size();

        //weak.resize(length*2);


        for (int i = 0; i < length; i++)
        {
            weak.push_back(weak[i]+n);
        }

        answer = length + 1;

        sort(dist.begin(), dist.end());

        do
        {
            for (int i = 0; i < length; i++)
            {
                int start = weak[i];
                int finish = weak[i + length - 1];

                for (int j = 0; j < dist.size(); j++)
                {
                    start += dist[j];
                    if (start >= finish)
                    {
                        answer = min(answer, j + 1);
                        break;
                    }

                    int next = upper_bound(weak.begin(), weak.end(), start) - weak.begin();
                    start = weak[next];
                }
            }
        } while (next_permutation(dist.begin(), dist.end()));

        if (answer == length + 1)
            return -1;

        return answer;
    }


# 22.01.07(금)
* 정말 어려운 문제였다. 완전탐색으로 풀면 되는 문제인 것을 알았으나 못풀었다.
* 원형을 *2 하여 일자로 만드는 기법이 이 문제의 핵심 인 것 같다.
* 또한 검사 시작 지점, 종료 예상 지점과 모든 지점 방문 완료 조건 코딩이 한번에 안되었는데 나중에 다시 이 문제를 풀었을때 바로 코딩할수있을 정도는 되어야 될 것 같다.
* 지금은 순열 함수인 next_permutation을 사용하였는데 조합에 대한 연구도 필요 할 듯
* upper_bound, lower_bound에 대해서 다시 공부 필요