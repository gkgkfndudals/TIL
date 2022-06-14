# 프로그래머스(카카오 2020년)  - 가사 검색

### 이 문제를 풀기 위한 과정
이 문제는 Trie 알고리즘을 이용하여 풀 수 있지만 익숙한 이진탐색을 이용하여서도 풀 수 있다.

1. 이진탐색으로 풀더라도 물음표가 앞에서부터 시작하는 케이스와 뒤에서부터 시작하는 케이스 두 개로 나누어 생각했어야 한다.
    * 물음표가 앞에서부터 시작하는 케이스
        - 글자를 뒤집고(reverseWords), 물음표가 시작하는 부분부터 'a'를 채워서 lower_bound로 lo 값 찾고, 'z'로 채워서 upper_bound로 hi 값 찾아야 한다.
        - 예를 들어 ????o 같은 경우, o???? 로 뒤집고 이 물음표 안에 패턴만 맞으면 되기 때문에 oaaaa ~ ozzzz 범위에 있는 word만 찾으면 되기 때문이다.
    * 물음표가 앞에서부터 시작하지 않는 케이스
        - 위에와 똑같이 생각하면 되는데, 대신에 기존에 있던 words 와 비교하면 된다.
2. upper_bound 는 찾으려는 key 값을 초과하는 값이 처음 나타나는 위치이고, lower_bound 는 찾으려는 Key 값 이상의 값이 처음 나타는 위치 이기 때문에 두 값을 빼주면 words 내지는 reverse_words 안에 있는 글자 중 해당 패턴에 맞는 글자의 개수가 나온다.
3. 마지막으로 hi - lo 값을 answer 에다 push 해주면 된다.

CODE1

    #include <string>
    #include <vector>
    #include <algorithm>
    #include <iostream>

    using namespace std;

    static bool cmp(string a, string b)
    {
        if (a.length() < b.length())
        {
            return true;
        }
        else if (a.length() == b.length())
        {
            return a < b;
        }
        return false;

    }

    vector<int> solution(vector<string> words, vector<string> queries) {
        vector<int> answer;
        
        vector<string> reverse_words = words;

        for (int i = 0; i < reverse_words.size(); i++)
        {
            reverse(reverse_words[i].begin(), reverse_words[i].end());
        }
        sort(words.begin(), words.end(), cmp);
        sort(reverse_words.begin(), reverse_words.end(), cmp);

        for (int i = 0; i < queries.size(); i++)
        {   
            string query = queries[i];
        
            int lo, hi;
            int idx;

            if (queries[i][0] == '?')
            {
                reverse(query.begin(), query.end());

                idx = query.find('?');

                for (int j = idx; j < query.size(); j++)
                {
                    query[j] = 'a';
                }
                lo = lower_bound(reverse_words.begin(), reverse_words.end(), query, cmp) - reverse_words.begin();

                for (int j = idx; j < query.size(); j++)
                {
                    query[j] = 'z';
                }
                hi = lower_bound(reverse_words.begin(), reverse_words.end(), query, cmp) - reverse_words.begin();
            }
            else
            {
                idx = query.find('?');
                
                for (int j = idx; j < query.size(); j++)
                {
                    query[j] = 'a';
                }
                lo = lower_bound(words.begin(), words.end(), query, cmp) - words.begin();
                
                for (int j = idx; j < query.size(); j++)
                {
                    query[j] = 'z';
                }
                hi = upper_bound(words.begin(), words.end(), query, cmp) - words.begin();
            }
            
            answer.push_back(hi - lo);
        }



        return answer;
    }

# 22.06.14(화)
* 20220609_CountSpecificNumSortedArray와 유사한 lower_bound, upper_bound을 이용하여 갯수를 구하는 문제이다.
* 이 문제에서 중요한 부분은 와일드 카드인 '?' 문자의 처리 방식이다. 문제 조건에서 문자단어는 소문자로만 구성되어 있다고 제한을 주었기 때문에 와일드카드 문자에 소문자 제일 작은 'a'와 제일 큰 'z'로 값을 바꿔서 문제를 해결 하였다.
* 또한, 와일드카드 문자는 접두어와 접미사에만 나오기 때문에 문자 반전(reverse)을 이용하여 문제를 해결하는 아이디어가 인상 깊었다. 
* 역시 카카오 문제 답게 아직 나에게는 많이 어려운 문제였다. 다시한번 이 문제를 꼭 풀어보도록 해야겠다.