#  백준 - 회전 초밥

### 이 문제를 풀기 위한 과정
투 포인터 알고리즘 문제! (시간복잡도 O(N))
이 문제는 부분 배열의 길이(K)가 고정적이여서 슬라이딩 윈도우으로도 풀 수 있지만 투포인터로 풀어봤다.  

K구간의 초밥중에서 C의 초밥이 있는지 구현하는데에 고민을 많이 했었다.  
처음에는 Map으로 풀던가, find함수를 이용하여 vector에 K구간 값을 넣어서 length(길이)를 구하려고 하였지만, 생각해보니 시간복잡도가 O(N*K)이 되지 않을까 걱정이 되었다.  
그래서 초밥 가짓수 D의 check배열을 만들어 O(1)만에 접근하여 만들어 시간복잡도를 줄어보았다.  
 
CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(int N, int K, int C, vector<int> vec);

    int main()
    {
        ios_base::sync_with_stdio(false);
        cin.tie(NULL);
        cout.tie(NULL);

        int N, D, K, C;

        cin >> N >> D >> K >> C;

        vector<int> vec;
        vec.assign(N, 0);

        for (int i = 0; i < N; i++)
        {
            int num;
            cin >> num;
            vec[i] = num;
        }

        int answer = solution(N, K, C, vec);

        cout << answer;
        return 0;
    }

    int solution(int N, int K, int C, vector<int> vec)
    {
        int check[3001];
        fill(check, check + 3001, 0);
        
        int start = 0;
        int end = 0;
        int cnt = 0;
        int ans = -1e9;
        int ans_temp = 0;

        while (start < N)
        {
            if (cnt < K)
            {
                end = end % N;

                int num = vec[end];
                if (check[num] == 0)
                {
                    ans_temp++;
                }
                check[num]++;
                cnt++;
                end++;
            }
            else if (cnt >= K)
            {
                if (check[C] != 0)
                {
                    ans = max(ans, ans_temp);
                }
                else if (check[C] == 0)
                {
                    ans = max(ans, ans_temp + 1);
                }
                
                int num = vec[start];
                check[num]--;
                if (check[num] == 0)
                {
                    ans_temp--;
                }

                cnt--;
                start++;
            }
        }

        return ans;
    }

    /*
    8 30 4 30
    7
    9
    7
    30
    2
    7
    9
    25
    */

# 22.11.16(수)
* https://velog.io/@codenmh0822/%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%94%A9-%EC%9C%88%EB%8F%84%EC%9A%B0-%EA%B5%AC%EA%B0%84-%ED%95%A9-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98 슬라이딩 윈도우, 투포인터 차이점