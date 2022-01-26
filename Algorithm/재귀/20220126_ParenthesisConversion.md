# 프로그래머스 - 괄호 변환

### 이 문제를 풀기 위한 과정
이 문제는 제시된 알고리즘을 재귀적으로 구현하여 해결 할 수 있다.
문제에 제시되어진 그대로 재귀함수를 이용하여 구현을 한다면 쉽게 해결 할 수 있는 문제이다.
"균형잡힌 괄호 문자열"의 인덱스를 반환하는 함수, "올바른 괄호 문자열"인지 판단하는 함수를 구현한다.

CODE1

    #include <string>
    #include <vector>
    #include <iostream>

    using namespace std;

    int Balanced_index(string p);
    bool Check_proper(string u);
    string solution(string p);

    int main()
    {
        string p = ")(";

        cout << solution(p);
    }

    string solution(string p) {
        string answer = "";
        
        if (p.compare("") == 0)
        {
            return answer;
        }

        int index = Balanced_index(p);
        
        string u = p.substr(0, index+1);
        string v = p.substr(index+1, p.length());

        if (!Check_proper(u))
        {
            string temp = "(";
            temp += solution(v);
            temp += ")";
            u = u.substr(1, u.length() - 1);
            u = u.substr(0, u.length()-1);

            for (int i = 0; i < u.length(); i++)
            {
                if (u[i] == '(')
                    u[i] = ')';
                else if (u[i] == ')')
                    u[i] = '(';
            }

            temp += u;
            
            answer += temp;
        }
        else 
        {
            answer = u + solution(v);
        }

        return answer;
    }

    int Balanced_index(string p)
    {
        int count = 0;

        for (int i = 0; i < p.length(); i++)
        {
            if (p[i] == '(')
                count++;
            else if (p[i] == ')')
                count--;

            if (count == 0)
                return i;
        }
    }

    bool Check_proper(string u) 
    {
        int count = 0;

        for (int i = 0; i < u.length(); i++)
        {
            if (u[i] == '(')
                count++;
            else
                if (count == 0)
                    return false;
                else
                    count--;
        }

        return true;
    }

# 22.01.26(수)
* 문제에 나와있는대로만 구현하면 되는 아주 쉬운 문제였지만, 문제를 이해를 못해서 어떻게 풀어야될지 감도 안잡힌 문제였다.
* 앞으로 재귀함수를 이용한 문제는 차근차근 읽어보며  이해하는데에 집중을 해야 될 것 같다.