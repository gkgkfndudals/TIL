# 프로그래머스 2018 KAKAO BLIND RECRUITMENT - 추석 트래픽
https://school.programmers.co.kr/learn/courses/30/lessons/17676

### 이 문제를 풀기 위한 과정
로그는 응답완료시간 기준으로 오름차순으로 정렬 되어 있다. 그러므로 특정 로그의 끝나는 기간에 +1sec의 값과 나머지 로그값들의 시작값을 비교한다고 생각하면 쉽다. 그러면서 특정 로그의 끝나는 값의 +1sec안에 들어가는 시작값이 몇개인지를 찾고 거기서 최대값을 찾아주면 됐다.  
시간을 토큰 할 때 ms단위를 생각하여 계산해 준다.  

CODE1
```java
import java.util.StringTokenizer;
import java.util.ArrayList;
// import java.util.Collections;

class Solution {
    public int solution(String[] lines) {
        if(lines.length == 1)
        {
            return 1;
        }
        
        int answer = 0;
        ArrayList<Pair> throughput = new ArrayList<>();
        
        for(int i = 0; i < lines.length; i++)
        {
            String input = lines[i];
            StringTokenizer st = new StringTokenizer(input);
            st.nextToken();
            String S = st.nextToken(); // 03:10:33.020
            String T = st.nextToken(); // 0.011s
            String time = "";
            st = new StringTokenizer(S, ".");
            String t = st.nextToken(); // 03:10:33
            String decimal = st.nextToken(); // 020
            
            st = new StringTokenizer(t, ":");
            int endSec = Integer.parseInt(st.nextToken()) * 3600000
                + Integer.parseInt(st.nextToken()) * 60000
                + Integer.parseInt(st.nextToken()) * 1000
                + Integer.parseInt(decimal);
            
          
            T = T.substring(0, T.length() - 1);
            int i_t = (int) (Double.parseDouble(T) * 1000);
            
            throughput.add(new Pair(endSec - i_t + 1, endSec));
        }
        
        for(int i =0; i < throughput.size(); i++)
        {
            int cnt = 1;
            for(int j = i+1; j < throughput.size(); j++)
            {
                if(throughput.get(i).end + 1000 > throughput.get(j).start)
                {
                    cnt++;
                }
            }
            
            answer = Math.max(answer, cnt);
        }
        
        return answer;
    }
    
    static class Pair {
        int start;
        int end;
        
        public Pair(int start, int end)
        {
            this.start = start;
            this.end = end;
        }
    }
}
```

# 23.02.19(일)
* 
