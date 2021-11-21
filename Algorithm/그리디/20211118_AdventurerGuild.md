# 알고리즘 - 모험가길드(나동빈 책)

### 이 문제를 풀기 위한 과정
1. 공포도를 기준으로 오름차순으로 정렬
2. 그룹에 포함된 모험가의 수가 현재 확인하고 있는 공포도보다 크거나 같다면, 그룹을 결성

CODE

    #include <iostream>
	#include <string>
	#include <vector>
	#include <algorithm>

	using namespace std;
	int N = 0;
	int ans = 0;

	int main(void)
	{
		int count = 0;

		vector<int> v;
		vector<int>::iterator itr;

		cin >> N;

		int panic;

		for (int i = 0; i < N; i++)
		{
			cin >> panic;
			v.push_back(panic);
		}
		
		sort(v.begin(), v.end());

		for (itr=v.begin(); itr != v.end(); itr++)
		{
			count++;
			if (count >= *itr) 
			{
				count = 0;
				ans++;
			}
			
		}
		
		cout << endl << ans << endl;
		return 0;
	}

# 21.11.21(일)
* 2021.11.18에 풀었던 문제를 오늘 올리는 하루, 인제부터 꾸준히 올리는 습관을 들이자!
* 처음으로 MarkDown을 사용해보고 익히는 뜻 깊은 하루