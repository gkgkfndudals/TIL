# 알고리즘 - 만들 수 없는 금액(나동빈 책)

### 이 문제를 풀기 위한 과정
1. 주어진 동전 리스트를 오름차순으로 sort() 한다.
2. 맨 처음 동전부터 차례대로 동전을 추가해가며 만둘 수 없는 금액을 찾는다.
3. 기존 target에 새 동전의 단위를 더하여 target을 업데이트
4. target보다 새로 추가한 동전의 금액이 크다면 만들 수 없는 금액이 나온다.

CODE

    #include <iostream>
    #include <vector>
    #include <algorithm>

    using namespace std;

    int main(void)
    {
        int ans = 1;

        vector<int> v;
        vector<int>::iterator itr;

        int arr[1000];
        int N;
        cin >> N;
        
        for (int i = 0; i < N; ++i) {
            cin >> arr[i];
            v.push_back(arr[i]);
        }
        
        sort(v.begin(), v.end());

        for (itr = v.begin(); itr != v.end(); itr++)
        {
            if (ans < *itr)
                break;

            ans = ans + *itr;

        }

        cout << ans;

        return 0;
    }

# 21.11.23(화)
*  target보다 새로 추가한 동전의 금액이 크다면 만들 수 없는 금액이 나온다. 이 부분에서 이해가 어려운 문제였다.
