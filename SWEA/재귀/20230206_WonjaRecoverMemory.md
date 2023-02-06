# SWEA 1289 - 원재의 메모리 복구하기

### 이 문제를 풀기 위한 과정
https://github.com/gkgkfndudals/TIL/blob/master/SWEA/%EC%99%84%EC%A0%84%ED%83%90%EC%83%89/WonjaRecoverMemory_1289.md  

옛날에는 완전탐색으로 풀었지만 이번에는 재귀로 풀어보았다.

CODE1
```java
    import java.util.*;
    import java.io.*;

    public class Solution {
        static int ans;
        
        public static void main(String[] args) throws Exception {
            // TODO Auto-generated method stub
            StringBuilder sb = new StringBuilder();
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            int T = Integer.parseInt(br.readLine());
            
            for(int test_case = 1; test_case <= T; test_case++)
            {
                ans = 0;
                String s = br.readLine();
                recursion(s, '0', 0);
                sb.append("#" + test_case + " " + ans + "\n");
            }
            
            System.out.println(sb.toString());
        }
        
        static void recursion(String s, char ch, int depth)
        {
            if(depth == s.length())
            {
                return;
            }
            
            if(s.charAt(depth) != ch)
            {
                ch = s.charAt(depth);
                ans++;
            }
            recursion(s, ch, depth + 1);
        }
    }
```

# 22.01.28(금)
* 다음에는 이 문제를 DFS으로도 풀수 있다고 하는데 풀어봐야겠다.