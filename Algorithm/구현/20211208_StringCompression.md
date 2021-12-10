# 프로그래머스 - 문자열 압축

### 이 문제를 풀기 위한 과정
이 문제는 문자열의 길이가 1000 이하이기 때문에 완전탐색을 수행을 할 수 있다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20211210_StringCompression.PNG)

위 사진의 strsub의 규칙성을 보고 이중 for문을 만들어 주면 간단하게 문제를 해결할수 있다.
1. vector에 비교할 문자열(previous)를 넣어 놓고 현재 K단위로 쪼개어진 문자열과 비교한다.
2. 같다면 num++을 해주고, 다르다면 vector에 있는 문자열을 pop하여 문자열을 붙여준다. num > 1이면 num도 붙인다.
3. 마지막으로 min 함수를 이용하여 최소길이의 값을 구해주면 끝~

CODE1

    #include <string>
    #include <vector>
    #include <iostream>
    using namespace std;
    int solution(string s);

    void main(void)
    {
        string s;
        s = "abaa";

        solution(s);
    }

    int solution(string s) {
        int answer = 1000;
        
        for (int k = 1; k <= s.size(); k++)
        {
            vector<string> v;
            vector<string>::iterator previos;
            int num = 1;
            string str="";

            for (int i = 1; i <= s.size(); i++)
            {
                if ((i - 1) * k <= s.size() && k <= s.size())
                {
                    string current = s.substr((i - 1) * k, k);

                    if (v.empty())
                    {
                        v.push_back(current);
                        continue;
                    }
                
                    previos = v.begin();
                    if (current.compare(*previos)==0)
                    {
                        num++;
                    }
                    else
                    {
                        
                        if (num > 1) {
                            str.append(to_string(num));
                        }
                        str.append(*previos);
                
                        v.pop_back();
                        v.push_back(current);
                        num = 1;
                    }
                    
                }  
            }
        
            if (num != 1)
                str += to_string(num);

            if (!v.empty())
            {
                previos = v.begin();
                str += *previos;
            }

            int i_length = str.length();
            answer = min(i_length, answer);
        }
        
        cout << answer;
        return answer;
    }

    
CODE2

다른 사람의 풀이 코드이다. 훨씬 깔끔하고 좋아보여 공부할겸 올려본다.
vector에 미리 문자열을 잘라서 다 넣어두고, 하나씩 빼면서 문자열을 비교하여 준다.

    #include <string>
    #include <vector>
    #include <iostream>

    using namespace std;

    vector<string> convert(string s, int n)
    {
        vector<string> v;
        for(int i = 0 ; i <s.length() ; i+=n)
        {
            v.push_back(s.substr(i,n));
        }
        return v;
    }

    int solution(string s) {
        int answer = 0;
        vector<string> tok;
        string before;
        int cnt = 1;
        int min = s.length();
        string str="";
        for(int j = 1 ; j <= s.length()/2 ; j++)
        {
            tok = convert(s,j);
            str = "";
            before = tok[0];
            cnt = 1;
            for(int i = 1 ; i < tok.size() ; i++)
            {
                if(tok[i] == before) cnt++;
                else
                {
                    if(cnt != 1) str += to_string(cnt);
                    str += before;
                    before = tok[i];
                    cnt = 1;
                }
            }
            if(cnt != 1)str += to_string(cnt);
            str += before;  
            min = min<str.length() ? min : str.length();
        }
        cout<<str;

        return min;
    }


# 21.12.10(금)
* 테스트케이스 3번이 안되어 살펴보니 마지막 문자열이 압축이 되면 num이 문자열에 append가 안되는 것을 확인하였다.
* 그래서 첫번째 for 문에서 num != 1 일때 num을 문자열에 붙여주었다.
