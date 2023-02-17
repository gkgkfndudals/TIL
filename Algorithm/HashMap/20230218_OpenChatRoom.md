# 프로그래머스 2019 KAKAO BLIND RECRUITMENT - 오픈채팅방
https://school.programmers.co.kr/learn/courses/30/lessons/42888

### 이 문제를 풀기 위한 과정
HashMap을 이용하여 (uid, name)을 관리해주면 쉽게 해결 할 수 있는 문제였다.  
Leave일때 map.remove(uid)를 해주어 실패가 많이 나왔었다.  
생각해보면 map에서 삭제해버리면 나중에 list에서 Leave의 문자열 답을 구할때 map.get(uid)를 할 수가 없다.  
처음에 왜 실패뜨는지 많이 당황을 하였다...

CODE1
```java
import java.util.StringTokenizer;
import java.util.HashMap;
import java.util.ArrayList;

class Solution {
    public String[] solution(String[] record) {
        String[] answer;
        HashMap<String, String> map = new HashMap<>();
        ArrayList<Pair> list = new ArrayList<>();
        
        for(int i = 0; i < record.length; i++)
        {
            StringTokenizer st = new StringTokenizer(record[i]);
            
            String oper = st.nextToken();
            String uid = st.nextToken();
            String name = "";
            while(st.hasMoreTokens())
            {
                name = st.nextToken();    
            }
             
            if(oper.equals("Enter")) {
                map.put(uid, name);
                list.add(new Pair(uid, "Enter"));
        
            }else if(oper.equals("Leave")) {
                // map.remove(uid); // 이거 때문에 실패 뜸
                list.add(new Pair(uid, "Leave"));
            
            } else if(oper.equals("Change")) {
                map.put(uid, name);
            }
        }
        
        
        ArrayList<String> result = new ArrayList<>();
        for(int i = 0; i < list.size(); i++)
        {
            Pair p = list.get(i);
            if(p.oper.equals("Enter"))
            {
                result.add(map.get(p.uid) +"님이 들어왔습니다.");
            } else if(p.oper.equals("Leave"))
            {
                result.add(map.get(p.uid) +"님이 나갔습니다.");
            }
        }
        
        answer = new String[result.size()];
        result.toArray(answer);
   
        return answer;
    }
    
    class Pair {
        String uid;
        String oper;
        
        public Pair(String uid, String oper)
        {
            this.uid = uid;
            this.oper = oper;
        }
    }
}
```

# 23.02.18(토)
* 
