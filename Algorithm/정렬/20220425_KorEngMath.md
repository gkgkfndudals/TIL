# 백준 - 국영수

### 이 문제를 풀기 위한 과정
N = 100,000 이므로 c++ 에서 지원하는 정렬 NlogN으로 500,000 시간복잡도가 나온다.

그리고 cmp를 이용하여 
1. 국어 점수를 내림차순으로 정렬
2. 국어 점수가 같으면 영어 점수를 오름차순으로 정렬
3. 영어 점수가 같으면 수학 점수를 내림차순으로 정렬

CODE1

    #include <iostream>
    #include <vector>
    #include <string>
    #include <algorithm>

    using namespace std;

    void solution();

    class Student
    {
    public:
        string name;
        int kor;
        int eng;
        int maths;
    };

    bool cmp(Student &s1, Student &s2)
    {
        if (s1.kor != s2.kor) return s1.kor > s2.kor;
        else
        {
            if (s1.eng != s2.eng) return s1.eng < s2.eng;
            else
            {
                if (s1.maths != s2.maths) return s1.maths > s2.maths;
                return s1.name < s2.name;
            }
        }
    }

    int N;
    vector<Student> students;

    int main()
    {
        ios::sync_with_stdio(false);
        cin.tie(NULL);

        cin >> N;

        students.assign(N, Student());

        for (int i = 0; i < N; i++)
        {
            cin >> students[i].name >> students[i].kor >> students[i].eng >> students[i].maths;
        }

        solution();


        return 0;
    }

    void solution()
    {
        sort(students.begin(), students.end(), cmp);

        for (int i = 0; i < N; i++)
        {
            cout << students[i].name << "\n";
        }

    }

# 22.04.22(금)
* endl을 하면 '시간초과'가 나오고 "\n"을 하면 정상통과가 되는데 왜 그러는지 찾아봤다.  
std::endl은 출력버퍼를 비우고, \n은 프로그램이 종료되면서 커널에 의해 버퍼를 비운다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220425_KorEngMath.png)

* cmp함수 매개변수 class, struct에서 주소값 & 을 붙이면 속도가 훨씬 빠른 것 을 확인하였다.  
앞으로 항상 주소값 &을 붙이는 습관을 꼭 들이자!! 