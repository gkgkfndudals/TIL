# 알고리즘 - 모험가길드(나동빈 책)

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