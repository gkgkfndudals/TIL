# 프로그래머스 - 무지의 먹방 라이브

### 이 문제를 풀기 위한 과정
이 문제는 시간이 적게 걸리는 음식부터 확인하는 탐욕적 접근 방식으로 해결할 수 있다.
1. 모든 음식을 시간을 기주능로 정렬 한 뒤, 시간이 적게 걸리는 음식부터 제거해 나가는 방식을 이용
2. 이를 위해 우선순위 큐를 이용하여 구현
3. '가장 적게 걸리는 음식의 시간 * 남은 음식의 개수'는 가장 적은 음식을 다 먹기 위해서 걸리는 시간
4. '전체시간 - 가장 적은 음식을 다 먹기 위해서 걸리는 시간'을 해준다.
5. '이때 현재 전체 남은 시간 < 다음으로 가장 적은 음식을 다 먹기 위해 걸리는 시간' 이라면 우선순위 큐에서 빼지않는다.
6. 매초 먹어야 할 음식들을 음식번호순으로 정렬한다.
7. 그리고 '다음으로 먹어야 할 음식의 번호'를 찾아 리턴한다.

CODE1

    #include <string>
    #include <iostream>
    #include <vector>
    #include <algorithm>
    #include <queue>
    using namespace std;

    long long sum(vector<int> food_times);
    int solution(vector<int> food_times, long long k);

    struct compareSecond {
        bool operator()(pair<int, int> a, pair<int, int>b) {
            return a.second > b.second;
        }
    };

    struct compareFirst {
        bool operator()(pair<int, int> a, pair<int, int>b) {
            return a.first > b.first;
        }
    };

    int solution(vector<int> food_times, long long k) {
        int answer = 0;

        if (sum(food_times) <= k)
            return -1;

        priority_queue< pair<int, int>, vector<pair<int, int>>, compareSecond> pq;
        priority_queue< pair<int, int>, vector<pair<int, int>>, compareFirst> pq_first;


        for (int i = 1; i <= food_times.size(); i++)
        {
            pq.push(make_pair(i, food_times.at(i - 1)));
        }
        
        int previous = 0;

        while ( (pq.top().second - previous) * pq.size() <= k)
        {
            if (pq.top().second - previous <= 0)
            {
                pq.pop();
                continue;
            }

            pair<int, int> p = pq.top();
            int i_pqCount = pq.size();

            int i_useTime = i_pqCount * (p.second - previous);

            previous = previous + (p.second - previous);

            k = k - i_useTime;
            pq.pop();
        }

        while (!pq.empty())
        {
            pair<int, int> p = pq.top();
            pq_first.push(p);
            pq.pop();
        }


        int index = k % pq_first.size();

        for (int i = 0; i < index; i++)
        {
            pq_first.pop();
        }

        answer = pq_first.top().first;
        
        return answer;
    }

    long long sum(vector<int> food_times)
    {
        long long sum = 0;
        vector<int>::iterator itr;
        for (itr = food_times.begin(); itr != food_times.end(); itr++)
        {
            sum += *itr;
        }

        return sum;
    }


# 21.12.01(수)
* 효율성 테스트에서 계속 실패가 났었다. 이유로는 시간 k의 자료형이 long long(8byte)이다. 그런데 나는 sum 함수를 int으로 리턴해주었다.
* 앞으로 시간 최적화 뿐만 아니라 자료형에 대해서 좀 더 유심히 보고 생각을 해야 될 것 같다.
* 카카오 문제중에서는 쉬운 문제라고 하는 것 같은데 난 무려 4일이나 걸렸다. 아직 부족한게 너무 많은 자신이 화가 난다.