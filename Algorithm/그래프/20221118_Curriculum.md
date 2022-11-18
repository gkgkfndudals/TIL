#  이코테 - 커리큘럼

### 이 문제를 풀기 위한 과정
이 문제는 위상 정렬 알고리즘의 응용문제이다.  
각 노드(강의)에 대하여 인접한 노드를 확인 할 때, 인접한 노드에 대하여 현재보다 강의 시간이 더 긴 경우를 찾는다면, 더 오랜 시간이 걸리는 경우의 시간 값을 저장하는 방식으로 결과 테이블을 갱신하여 답을 구 할 수 있다.  
따라서 위상 정렬을 수행하면서, 매번 간선 정보를 확인하여 결과 테이블을 갱신한다.  

최종적으로 각 강의를 수강하기까지의 최소 시간을 ans 벡터에 담도록 하였다.  
또한 처음에 각 강의 시간은 time 벡터에 담겨 있는데, 위상 정렬 함수의 초기 부분에서 DeepCopy로 복사하여 ans 벡터 값으로 설정하는 작업을 수행하였다.

CODE1

    #include <iostream>
    #include <vector>
    #include <queue>

    using namespace std;

    vector<int> solution(int N, vector<vector<int>> graph, vector<int> time, vector<int> indegree);

    int main(void)
    {
        int N;
        cin >> N;

        vector<vector<int>> graph;
        graph.assign(N+1, vector<int>(0, 0));

        vector<int> time;
        time.assign(N + 1, 0);
        vector<int> indegree;
        indegree.assign(N + 1, 0);

        for (int i = 1; i < N + 1; i++)
        {
            int t;
            cin >> t;
            time[i] = t;

            while (true)
            {
                int n;
                cin >> n;

                if (n == -1)
                {
                    break;
                }
                graph[n].push_back(i);
                indegree[i] += 1;
            }
        }

        vector<int> answer = solution(N, graph, time, indegree);

        for (int i = 1; i < answer.size(); i++)
        {
            cout << answer[i] << endl;
        }
    }

    vector<int> solution(int N, vector<vector<int>> graph, vector<int> time, vector<int> indegree)
    {
        vector<int> ans;
        ans.assign(time.begin(), time.end());
        queue<int> q;
        
        for (int i = 1; i < indegree.size(); i++)
        {
            if (indegree[i] == 0)
            {
                q.push(i);
            }
        }

        while (!q.empty())
        {
            int now = q.front();
            q.pop();

            for (int i = 0; i < graph[now].size(); i++)
            {
                int num = graph[now][i];

                ans[num] = max(ans[num], ans[now] + time[num]);
                indegree[num]--;

                if (indegree[num] == 0)
                {
                    q.push(num);
                }
            }
        }

        
        return ans;
    }

    /*
    5
    10 -1
    10 1 -1
    4 1 -1
    4 3 1 -1
    3 3 -1
    */

# 22.11.18(금)
* 