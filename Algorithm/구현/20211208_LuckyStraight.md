# 백준 - 럭키 스트레이트

### 이 문제를 풀기 위한 과정
이 문제는 문제에서 요구하는 바를 그대로 구현하면 해결할 수 있다.
1. 정수형 데이터가 입력으로 들어왔을 때, 이를 각 자릿수로 구분하여 합을 계산한다.
2. 문자를 substr()으로 반으로 쪼개어 준다.
3. 각 문자를 하니씩 확인하며 정수형으로 변환한 뒤에 그 값을 합 변수에 더할 수 있다.

CODE1

    #pragma warning(disable:4996)
    #include <iostream>
    #include <string>
    using namespace std;

    int N;
    string ans;

    int main(void) 
    {
        cin >> N;

        string s = to_string(N);
        string str_front, str_end;
        
        str_front = s.substr(0, s.size() / 2);
        str_end = s.substr(s.size() / 2, s.size());
        
        int i_front=0, i_end=0;

        for (int i = 0; i < s.size() / 2; i++)
        {
            i_front += str_front.at(i)-'0';
            i_end += str_end.at(i) - '0';
        }

        if (i_front == i_end)
        {
            ans = "LUCKY";
        }
        else
        {
            ans = "READY";
        }

        cout << ans;

        return 0;
    }


# 21.12.01(수)
* 다시 한번 풀어보는 백준 문제였다. 옛날에는 자바로 코테를 준비하였는데 지금 c++으로 준비 중이다 보니 문자열 함수의 사용이 익숙치 않아 시간이 생각보다 너무 오래걸려버렸다.
* c++으로 문자열 문제를 많이 풀어봐야 될 것 같다. 정 어려우면.... 파이썬도 고려해 봐야 될 것 같다.