#  백준 - 플로이드

### 이 문제를 풀기 위한 과정
이 문제에서는 학생의 수 N이 500이하의 정수이므로 O(N^3)의 시간 복잡도로 동작하는 플로이드 워셜을 이용 할 수 있다.  
학생들의 성적을 비교한 결과를 방향 그래프 형태로 표현 할 수 있다. 성적이 낮은 학생이 성적이 높은 학생을 가리키는 방향 그래프로 표현할 수 있다.  

1. A에서 B로 도달이 가능하거나, B에서 A로 도달이 가능하면 '성적 비교'가 가능하다.  
2. 반대로 A에서 B로 도달이 불가능 하며, B에서 A로도 도달이 불가능하다면, '성적 비교 결과를 알 수 없는' 경우가 된다.  
3. 플로이드 워셜 알고리즘을 수행한 뒤에, 모든 노드에 대하여 다른 노드와 서로 도달이 가능한지를 체크하여 문제를 해결
4. 자기 자신은 항상 도달이 가능하다고 보고, 카운트를 진행한다.
5. 특정한 노드의 카운트 값이 N이라면, 해당 노드의 정확한 순위를 알 수 있다는 것을 의미한다.  

CODE1

    #include <iostream>
    #include <vector>

    using namespace std;

    int solution(int N, vector<vector<int>> graph);

    int main(void)
    {
        int N, M;
        cin >> N >> M;

        vector<vector<int>> graph;
        graph.assign(N + 1, vector<int>(N + 1, 1e9));

        for (int i = 0; i < N + 1; i++)
        {
            graph[i][i] = 0;
        }

        for (int i = 0; i < M; i++)
        {
            int s, e;
            cin >> s >> e;
            graph[s][e] = 1;
        }

        int answer = solution(N, graph);

        cout << answer;
    }

    int solution(int N, vector<vector<int>> graph)
    {
        int answer = 0;

        for (int k = 1; k < N + 1; k++)
        {
            for (int i = 1; i < N + 1; i++)
            {
                for (int j = 1; j < N + 1; j++)
                {
                    graph[i][j] = min(graph[i][j], graph[i][k] + graph[k][j]);
                }
            }
        }

        for (int i = 1; i < N + 1; i++)
        {
            int cnt = 0;

            for (int j = 1; j < N + 1; j++)
            {
                if (graph[i][j] != 1e9 or graph[j][i] != 1e9)
                {
                    cnt += 1;
                }
            }

            if (cnt == N)
            {
                answer += 1;
            }
        }

        return answer;
    }

    /*
    6 6
    1 5
    3 4
    4 2
    4 6
    5 2
    5 4
    */


# 22.07.29(금)
* A -> B, B - > A 로 갈 수가 없다면 성적 비교를 할 수 없다라는 부분이 중요한 포인트이다.
* graph[i][j] != 1e9 or graph[j][i] != 1e9  