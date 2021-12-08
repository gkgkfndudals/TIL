# 알고리즘 - 문자열 재정렬(나동빈 책)

### 이 문제를 풀기 위한 과정
이 문제는 문제에서 요구하는 바를 그대로 구현하면 해결할 수 있다.
1. 문자열이 입력되었을 때 문자를 하나씩 확인한 뒤
2. 숫자인 경우 따로 합계를 계산
3. 알파벳인 경우 별도의 리스트에 저장.
4. 리스트에 저장된 알파벳들을 정렬해 출력, 합계를 뒤에 붙여서 출력

CODE1

    #pragma warning(disable:4996)
    #include <iostream>
    #include <string>
    #include <algorithm>
    #include <vector>
    using namespace std;

    int main(void)
    {
        string s;
        int i_sum = 0;
        vector<string> v;
        vector<string>::iterator iter;
        string ans;

        cin >> s;

        string s_temp;
        for (int i = 0; i < s.size(); i++)
        {
            if (s.at(i) >= 48 && s.at(i) <= 57)
            {
                i_sum += s.at(i)-'0';
            }
            else
            {
                s_temp = s.at(i);
                v.push_back(s_temp);
            
            }
        }
        
        sort(v.begin(), v.end());

        for (iter = v.begin(); iter != v.end(); iter++) {
            ans.append(*iter);
        }

        ans.append(to_string(i_sum));
        
        cout << ans;
        return 0;
    }


# 21.12.08(수)
* 동빈나 책 문제인데 엄청 쉬운 문제였다. 백주으로 치면 브론즈4 일 것 같다.