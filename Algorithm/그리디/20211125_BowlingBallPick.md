# 알고리즘 - 볼링공 고르기(나동빈 책)

### 이 문제를 풀기 위한 과정
처음에 조합 문제 인줄 알고 조합으로 문제를 풀었다. CODE1은 조합으로, CODE2는 그리디 방법으로 문제를 품
1. 먼저 무게마다 볼링공이 몇 개 있는지를 계산해야 한다.
2. A가 특정한 무게의 볼링공을 선택했을 때, 이어서 B가 볼링공을 선택하는 경우를 차례대로 계싼하여 문제를 해결
2. 무게가 i인 볼링공의 갯수를 제외 하여
3. B가 선택하는 경우의 수와 곱한다.

CODE1

    #include <iostream>
    #include <string>
    #include <vector>
    #include <algorithm>
    using namespace std;

    int M, N;
    vector<int> v;
    int K;
    int arr[1000];
    int ans = 0;

    void sol(int idx, int depth);
    bool check(int arr[], int num, int depth);

    int main()
    {
        cin >> N >> M;

        for (int i = 0; i < N; i++) 
        {
            cin >> K;
            v.push_back(K);
        }
        
        //sort(v.begin(), v.end());
        
        sol(0, 0);
        
        cout << ans;
    }

    void sol(int idx, int depth)
    {
        vector<int>::iterator itr;

        if (depth == 2)
        {
            /*for (int i = 0; i < 2; i++)
                cout << arr[i];
            
            cout << endl;*/
            ans++;
            return;
        }

        for (int i=idx; i<N; i++)
        {
            if (check(arr, v.at(i), depth) == false)
                continue;
            arr[depth] = v.at(i);
            idx++;
            sol(idx, depth + 1);
        }
    }

    bool check(int arr[], int num, int depth) {
        for (int i = 0; i < depth; i++) {
            if (arr[i] == num)
                return false;
        }
        return true;
    }

CODE2

    #include <iostream>
    #include <string>
    using namespace std;

    int M, N;
    int K;
    int arr[1000] = { 0 };
    int ans = 0;

    int main()
    {
        cin >> N >> M;
        
        for (int i = 0; i < N; i++)
        {
            cin >> K;
            arr[K]++;
        }

        for (int num : arr) 
        {
            N -= num;
            ans += num * N;
        }

        cout << ans;
        
    }

# 21.11.23(화)
*  조합 문제인줄 알고 조합으로 풀었는데, 각 무게에 해당하는 볼링공의 개수를 카운트하여 그리디으로 풀 수 있는 방법을 찾아서 공부하였다.
* 1 ~ 10 까지의 숫자가 나오면 배열을 이용하여 문제를 접근하도록 하는 습관을 들이면 좋을 것 같다.
