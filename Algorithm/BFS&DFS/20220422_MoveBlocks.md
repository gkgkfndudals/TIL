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

    #include <string>
    #include <vector>
    #include <queue>

    using namespace std;

    #define HORIZ 0
    #define VER 1

    int dir_x[] = {0, -1, 0, 1};
    int dir_y[] = {-1, 0, 1, 0};

    int N;
    vector<vector<vector<bool>>> visited;

    struct Pos {
        int x;
        int y;
        //int dir;
    };

    class Robot
    {
        public:
            Pos part1;
            Pos part2;
            int shape; //가로 0, 세로 1
            int time;
        
        Robot(Pos part1, Pos part2, int shape, int time = 0)
        {
            this->part1 = part1;
            this->part2 = part2;
            this->shape = shape;
            this->time = time;
        }
        
    };


    bool possible(vector<vector<int>> board, Pos part1, Pos part2);

    int solution(vector<vector<int>> board) {
        int answer = 0;

        N = board.size();
        visited.assign(N, vector<vector<bool>>(N, vector<bool>(2, false)));

        queue<Robot> q;
    
        Robot start({ 0, 0 }, { 0, 1 }, HORIZ);

        q.push(start);
        
        while(!q.empty())
        {
            Robot now = q.front();
            q.pop();
            
            // 로봇이 차지하는 두 칸 중 어느 한 칸이라도 (N, N) 위치에 도착하면 됩니다.
            if((now.part1.x == N-1 && now.part1.y == N-1) || (now.part2.x == N-1 && now.part2.y == N-1))
            {
                answer = now.time;
                break;
            }
            
            for(int i=0; i<4; i++)
            {
                Pos new_part1{now.part1.x + dir_x[i], now.part1.y + dir_y[i]};
                Pos new_part2{now.part2.x + dir_x[i], now.part2.y + dir_y[i]};
    
                if(!possible(board, new_part1, new_part2))
                    continue;
                if(visited[new_part1.x][new_part1.y][now.shape] && visited[new_part2.x][new_part2.y][now.shape])
                    continue;
                
                Robot new_Robot(new_part1, new_part2, now.shape, now.time+1);
                q.push(new_Robot);
                visited[new_part1.x][new_part1.y][now.shape] = true;
                visited[new_part2.x][new_part2.y][now.shape] = true;
            }
            
            if(now.shape == HORIZ) //가로
            {
                //위
                Pos left_up{now.part1.x-1, now.part1.y};
                Pos right_up{now.part2.x-1, now.part2.y};
                if(possible(board, left_up, right_up)) 
                {
                    if(!visited[left_up.x][left_up.y][VER] || !visited[now.part1.x][now.part1.y][VER] ) // 왼쪽 축으로 위로
                    {
                        q.push(Robot(left_up, now.part1, VER, now.time+1));
                        visited[left_up.x][left_up.y][VER] = true;
                        visited[now.part1.x][now.part1.y][VER] = true;
                    }
                    if(!visited[right_up.x][right_up.y][VER] || !visited[now.part2.x][now.part2.y][VER] ) // 오른쪽 축으로 위로
                    {
                        q.push(Robot(right_up, now.part2, VER, now.time+1));
                        visited[right_up.x][right_up.y][VER] = true;
                        visited[now.part2.x][now.part2.y][VER] = true;
                    }
                }
                
                //아래
                Pos left_down{now.part1.x+1, now.part1.y};
                Pos right_down{now.part2.x+1, now.part2.y};
                if(possible(board, left_down, right_down))
                {
                    if(!visited[left_down.x][left_down.y][VER] || !visited[now.part1.x][now.part1.y][VER])// 왼쪽 축으로 아래로
                    {
                        q.push(Robot(left_down, now.part1, VER, now.time + 1));
                        visited[left_down.x][left_down.y][VER] = true;
                        visited[now.part1.x][now.part1.y][VER] = true;
                    }
                    if(!visited[right_down.x][right_down.y][VER] || !visited[now.part2.x][now.part2.y][VER])// 오른쪽 축으로 아래로
                    {
                        q.push(Robot(right_down, now.part2, VER, now.time + 1));
                        visited[right_down.x][right_down.y][VER] = true;
                        visited[now.part2.x][now.part2.y][VER] = true;
                    }
                }
                
            }
            
            if(now.shape == VER) //세로
            {
                //왼쪽
                Pos up_left{now.part1.x, now.part1.y - 1};
                Pos down_left{now.part2.x, now.part2.y - 1};
                if(possible(board, up_left, down_left)) 
                {
                    if(!visited[up_left.x][up_left.y][HORIZ] || !visited[now.part1.x][now.part1.y][HORIZ] ) // 위쪽 축으로 왼쪽
                    {
                        q.push(Robot(up_left, now.part1, HORIZ, now.time+1));
                        visited[up_left.x][up_left.y][HORIZ] = true;
                        visited[now.part1.x][now.part1.y][HORIZ] = true;
                    }
                    if(!visited[down_left.x][down_left.y][HORIZ] || !visited[now.part2.x][now.part2.y][HORIZ] ) // 밑쪽 축으로 왼쪽
                    {
                        q.push(Robot(down_left, now.part2, HORIZ, now.time+1));
                        visited[down_left.x][down_left.y][HORIZ] = true;
                        visited[now.part2.x][now.part2.y][HORIZ] = true;
                    }
                }
                
                //오른쪽
                Pos up_right{now.part1.x, now.part1.y + 1};
                Pos down_right{now.part2.x, now.part2.y + 1};
                if(possible(board, up_right, down_right))
                {
                    if(!visited[up_right.x][up_right.y][HORIZ] || !visited[now.part1.x][now.part1.y][HORIZ])// 위쪽 축으로 오른쪽으로
                    {
                        q.push(Robot(up_right, now.part1, HORIZ, now.time + 1));
                        visited[up_right.x][up_right.y][HORIZ] = true;
                        visited[now.part1.x][now.part1.y][HORIZ] = true;
                    }
                    if(!visited[down_right.x][down_right.y][HORIZ] || !visited[now.part2.x][now.part2.y][HORIZ])// 아래쪽 축으로 오른쪽으로
                    {
                        q.push(Robot(down_right, now.part2, HORIZ, now.time + 1));
                        visited[down_right.x][down_right.y][HORIZ] = true;
                        visited[now.part2.x][now.part2.y][HORIZ] = true;
                    }
                }
            }
            
        }
        
        return answer;
    }

    bool possible(vector<vector<int>> board, Pos part1, Pos part2)
    {
        if (N <= part1.x || part1.x < 0 || N <= part1.y || part1.y < 0
            || N <= part2.x || part2.x < 0 || N <= part2.y || part2.y < 0)
        {
            return false;
        }

        if (board[part1.x][part1.y] == 1 || board[part2.x][part2.y] == 1)
        {
            return false;
        }

        return true;
    }

# 22.04.22(금)
* 일반적인 1x1의 DFS/BFS가 아닌 1x2의 DFS/BFS 문제들도 많이 나오는 것 같다. 
* 이와 같은 문제가 나오면 항상 Shape도 생각하여 3차원 배열을 만들 생각을 떠올리자.
* 그리고 상하좌우 뿐만 아니라 회전에 대한 조건들도 생각하여 queue에 추가해주는 것도 꼭 생각하자.
* 특히 ‘회전’을 구현하는 부분이 좀 힘들었다. 조건들이 빡구현 느낌이 강하여 상당히 시간을 많이 보내었다.