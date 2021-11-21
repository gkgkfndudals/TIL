# 알고리즘 - 모험가길드(나동빈 책)

#이 문제를 풀기 위한 과정
1. 톱니바퀴의 극, 회전방향, 바퀴 번호를 구조체 벡터로 관리하기
2. 회전 정보를 관리하기

code 1

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

code 3 // 정상적으로 출력