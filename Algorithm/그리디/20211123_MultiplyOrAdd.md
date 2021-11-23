# 알고리즘 - 곱하기 혹은 더하기(나동빈 책)

### 이 문제를 풀기 위한 과정
1. 일반적으로 특정한 두 수에 대하여 연산을 수행할 때, 대부분은 곱하기가 더 값을 크게 만든다.
2. 하지만 두 수 중에서 하나라도 0, 1인 경우, 곱하기보다는 더하기를 수행하는 것이 효율적이다.
3. 그러므로, 두 수중에서 하나라도 1 이하인 경우에는 더하며, 두 수가 모두 2이상인 겨웅에는 곱하기를 하면 된다.

CODE
    #include <iostream>
    #include <string>
    using namespace std;

    string s;

    int main() 
    {
        int result = 0;

        cin >> s;

        result = s[0] - '0';

        for(int i=1; i<s.length(); i++)
        {
            if (s[i] <= 1 || result<= 1)
            {
                result = result + (s[i]-'0');
            }
            else
            {
                result = result * (s[i] - '0');
            }
        }

        cout << result;

        return 0;
    }

# 21.11.21(일)
* 곱하기가 일반적으로 더하기 보다 큰 수가 나오는 원리를 이용한 그리디 문제였다.