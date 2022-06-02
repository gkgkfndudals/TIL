# 프로그래머스 - 실패율(2019년 카카오)

### 이 문제를 풀기 위한 과정
스테이지 번호(i)를 1부터 N까지 증가시키며, 해당 단계에 머물러 있는 플레이어들의 수(count)를 계산한다.
그러한 플레이어들의 수(count) 정보를 이용하여 모든 스테이지에 ㄸ른 실패율을 계산한 뒤에 저장하면 된다.

하지만, 나는 algorithm 헤더에 있는 count 함수를 몰라 다른 방법으로 접근하였다.
stages를 오름차순으로 정렬한 뒤, 이진탐색의 upper_bound를 이용하여 플레이어들의 수(count) 정보를 구하였다. 

CODE1

    #include <string>
    #include <vector>
    #include <algorithm>
    #include <iostream>

    using namespace std;

    static bool cmp(pair<int, double> &a, pair<int,double> &b)
    {
        if(a.second == b.second)
            return a.first < b.first;
        return a.second > b.second;
    }

    vector<int> solution(int N, vector<int> stages) {
        vector<int> answer;

        sort(stages.begin(), stages.end());

        vector<pair<int, double>> vec;
        
        int previous = 0;
        

        for (int i = 1; i <= N; i++)
        {
            int idx = upper_bound(stages.begin(), stages.end(), i) - stages.begin();
            double clear_not = idx - previous;
            double clear = stages.size() - previous;
            double failure = clear_not/clear;

            if(clear == 0)
                failure = 0;
            
            previous = idx;
            
            vec.push_back(make_pair(i, failure));
        }
        
        sort(vec.begin(), vec.end(), cmp);
        
        for(int i=0; i<vec.size(); i++)
        {
            pair<int, double> p = vec[i];
            answer.push_back(p.first);
        }

        return answer;
    }

# 22.06.02(목)
* upper_bound, lower_bound에 대해서 나중에 다시 한번 복습해보자.