# 프로그래머스 - 자물쇠와 열쇠

### 이 문제를 풀기 위한 과정
자물쇠와 열쇠의 크기가 20 X 20 이므로 완전탐색으로도 충분히 풀 수 있는 문제이다.
열쇠를 회전시켜서 자물쇠에 끼워보는 작업을 전부 시도해보는 접근 방법을 이용할 수 있다.
그전에 2차원 배열의 회전 알고리즘에 대해서 알아야 된다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20211210_LotationArray.png)

CODE 

    vector<vector<int>> rotation(vector<vector<int>> key)
    {
        int N = key.size();
        int M = key[0].size();
        vector<vector<int>> rotation_key(N, vector<int>(M));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                rotation_key[j][N - 1 - i] = key[i][j];
            }
        }

        return rotation_key;
    }

이렇게 인덱스의 규칙을 찾아내서 코드로 짜주면 된다. 2차원 배열의 회전은 많이 쓰이는 것 이므로 외워두도록 하자
코테는 시간이 생명이므로... 오늘같이 여기에 시간을 보내면 안된다....

자물쇠와 열쇠 풀이법에 대해서 정리하겠다.

![](https://github.com/gkgkfndudals/TIL/blob/master/Algorithm/img/img_20211210_LockAndKey.png)

1. (M-1)*2 + N 인 전체 2차원 배열을 만들어 준다.
2. 열쇠를 전체 2차원 배열의 (0,0)부터 열쇠를 회전을 하면서 끼워 넣어본다.
3. 자물쇠 부분이 전체가 1이 되면 return true를 해주면 된다.
4. 문제에서 자물쇠의 돌기와 열쇠의 돌기가 만나면 안된다고 하므로 XOR 연산을 이용하여 준다.

CODE

    #include <iostream>
    #include <string>
    #include <vector>
    using namespace std;

    bool solution(vector<vector<int>> key, vector<vector<int>> lock);
    vector<vector<int>> rotation(vector<vector<int>> key);
    vector<vector<int>> insert_key(vector<vector<int>> v, vector<vector<int>> key, int iIndex, int jIndex);
    bool match(vector<vector<int>> v, int lockLen, int keyLen);

    int main(void)
    {
        vector<vector<int>> key;
        vector<int> key0 = { 0, 0, 0 };
        vector<int> key1 = { 1, 0, 0 };
        vector<int> key2 = { 0, 1, 1 };
        key.push_back(key0);
        key.push_back(key1);
        key.push_back(key2);

        vector<vector<int>> lock;
        vector<int> lock0 = { 1, 1, 1 };
        vector<int> lock1 = { 1, 1, 0 };
        vector<int> lock2 = { 1, 0, 1 };
        lock.push_back(lock0);
        lock.push_back(lock1);
        lock.push_back(lock2);

        solution(key, lock);
    }

    bool solution(vector<vector<int>> key, vector<vector<int>> lock) {
        bool answer = false;

        int N = lock.size();
        int M = key.size();
        int totalLen = (M - 1) * 2 + N;
        vector<vector<int>> v(totalLen, vector<int>(totalLen));
        vector<vector<int>> tempVec(totalLen, vector<int>(totalLen));

        for (int i = 0; i < lock.size(); i++)
        {
            for (int j = 0; j < lock.size(); j++)
            {
                v[i + M - 1][j + M - 1] = lock[i][j];
            }
        }

        vector<vector<int>> rotation_key = key;


        for (int i = 0; i < v.size(); i++)
        {
            for (int j = 0; j < v.size(); j++)
            {
                for (int k = 0; k < 4; k++)
                {
                    rotation_key = rotation(rotation_key);
                    tempVec = insert_key(v, rotation_key, i, j);
                    if (match(tempVec, N, M) == true)
                        answer = true;
                }
            }
        }

        cout << answer;
        return answer;
    }

    vector<vector<int>> rotation(vector<vector<int>> key)
    {
        int N = key.size();
        int M = key[0].size();
        vector<vector<int>> rotation_key(N, vector<int>(M));

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                rotation_key[j][N - 1 - i] = key[i][j];
            }
        }

        return rotation_key;
    }

    vector<vector<int>> insert_key(vector<vector<int>> v, vector<vector<int>> key, int iIndex, int jIndex)
    {
        for (int i = 0; i < key.size(); i++)
        {
            for (int j = 0; j < key.size(); j++)
            {
                if(iIndex+i < v.size() && jIndex+j < v.size())
                    v[iIndex + i][jIndex + j] = v[iIndex + i][jIndex + j]^key[i][j];
            }
        }

        return v;
    }

    bool match(vector<vector<int>> v, int lockLen, int keyLen)
    {
        int totalLen = v.size();
        for (int i = keyLen - 1; i < totalLen - (keyLen - 1); i++)
        {
            for (int j = keyLen - 1; j < totalLen - (keyLen - 1); j++)
            {
                if (v[i][j] == 1)
                    continue;
                else if (v[i][j] == 0)
                    return false;
            }
        }

        return true;
    }


# 21.12.10(금)
* 2차원 배열 회전을 꼭 외우도록 하자.
* 이 문제에서 제일 중요한 포인트라고 생각하는 부분은 (M-1)*2+N 의 길이를 가지는 전체 2차원 배열을 만들어주는 것이라고 생각한다.
* insert_key 함수에서 if(iIndex+i < v.size() && jIndex+j < v.size()) 을 빼먹어 인덱스 오류가 났었다. 열쇠가 전체 2차원 배열의 크기를 넘었기 때문이었다.