# 프로그래머스 - 블록 이동하기(2020년 카카오 신입 공채 1차)

### 이 문제를 풀기 위한 과정
문제는 일반적인 BFS 문제 풀듯이 풀면 된다. 그러나 주의 깊게 생각해야 할 부분은 다음과 같다.

1. 로봇은 회전이 가능하기 때문에 현재 위치에서 로봇이 회전된 위치들 또한 큐에 삽입하여야 한다.
2. 로봇은 두 파트로 이루어져 있기 때문에 2 개의 좌표를 차지한다. 따라서 방문 체크를 어떻게 할 것인지 신경 써야 한다. 로봇이 “두 파트 동시에 있었던 두 좌표”는 재방문하면 최단경로를 구할 수 없기 떄문에 재방문 하지 않도록 해야 한다.

방향까지 고려한 3 차원 배열 (visited[x][y][가로 or 세로])로 방문 체크하는 방법. 로봇의 두 파트는 왼쪽, 오른쪽 혹은 위쪽 아래쪽으로 구분 할 수 가 있다. 따라서 방향까지 고려하여 두 파트 각각 좌표 방문 체크를 해주는 것.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220422_MoveBlocks1.png)
![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220422_MoveBlocks2.png)

* 로봇이 1 초로 움직여 갈 수 있는 위치들
    + 4 가지 종류의 “이동” : 상, 하, 좌, 우
        - 로봇의 두 파트 모두가 갈 수 있는 곳이어야 한다.
    + 4 가지 종류의 “90도 회전” : 상, 하, 좌, 우
        - 가로 방향인 로봇의 경우 (90도 회전이므로 상하 회전만 가능)
            - 위로 회전하는 2 가지 경우 모두 위 두칸, 아래로 회전하는 2 가지 경우 모두 아래 두칸이 막혀있지 않아야 한다.
            - 회전하여 옮겨질 일부 한 파트가 회전하여 갈 예정인 곳도 갈 수 있는 곳이어야 한다.
        - 세로 방향인 로봇의 경우 (90도 회전이므로 좌우 회전만 가능)
            - 오른쪽으로 회전하는 2 가지 경우 모두 오른쪽 두 칸, 왼쪽으로 회전하는 2 가지 경우 모두 왼쪽 두 칸이 막혀있지 않아야 한다.
            - 회전하여 옮겨질 일부 한 파트가 회전하여 갈 예정인 곳도 갈 수 있는 곳이어야 한다.
최대 8 개의 로봇 위치를 큐에 삽입할 수 있다. 이 8 가지 후보를 로봇이 추후 갈 수 있는지 검사를 모두 진행해야 한다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20220422_MoveBlocks3.png)

3 차원 배열을 쓰지 않고 2 차원 배열, 즉 위치 좌표로만 방문 체크를 했다면 로봇이 위 그림에서처럼 1번, 2번 이렇게 움직였다면 3 번은 이미 방문했던 곳으로 판단되어 로봇이 3 번 위치로 이동하지 못한다. 실제로 가능해야하는데도 말이다. 3 번의 두 일부분이 각각 1번, 2번에 의해 방문 처리가 되었기 때문이다. 따라서 배열로 방문 체크를 하기 위해선 “모양” 까지 체크해야할 정보가 더 필요하다. 그래서 Robot 클래스에 Shape 변수 추가와 visited의 3번째 방에 모양을 저장한다.

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