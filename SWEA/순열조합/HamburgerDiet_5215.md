#  SWEA - 햄버거 다이어트 (5215)

### 이 문제를 풀기 위한 과정
이 문제는 쪼갤수 없는 0-1 배낭 문제이다.  
0-1 배낭 문제는 완전탐색, 이진탐색, DP 3가지 방법으로 풀 수 있다.  

하지만 해당 문제는 N이 최대 20이므로 조합으로 풀었다. O(2^20) => 약 100만

CODE1

    import java.util.*;
    import java.io.*;

    class Solution {
        static class Burger {
            int T;
            int K;

            public Burger(){}
            
            public int getT() {
                return T;
            }

            public void setT(int t) {
                T = t;
            }

            public int getK() {
                return K;
            }

            public void setK(int k) {
                K = k;
            }

        }

        static int N, L;
        static Burger[] burger;
        static int ans = Integer.MIN_VALUE;
        
        public static void main(String args[]) throws Exception {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            StringBuilder sb = new StringBuilder();
            
            int T;
            T = Integer.parseInt(br.readLine());
            

            for (int test_case = 1; test_case <= T; test_case++) {
                ans = 0; // 이거 때문에 처음 제출한 코드도 에러났다....
                StringTokenizer st = new StringTokenizer(br.readLine()); // 이거 때문에 처음 제출한 코드도 에러났다....
                N = Integer.parseInt(st.nextToken()); // 이거 때문에 처음 제출한 코드도 에러났다....
                L = Integer.parseInt(st.nextToken()); // 이거 때문에 처음 제출한 코드도 에러났다....
                burger = new Burger[N];

                for (int i = 0; i < N; i++) {
                    st = new StringTokenizer(br.readLine());
                    burger[i] = new Burger();
                    burger[i].setT(Integer.parseInt(st.nextToken()));
                    burger[i].setK(Integer.parseInt(st.nextToken()));
                }

                combination(0, 0, 0);
                sb.append("#" + test_case + " " + ans + "\n"); 
            }
            
            System.out.println(sb.toString());
        }

        static void combination(int idx, int calorie, int score) {
            if (calorie > L) {
                return;
            }
            else
            {
                ans = Math.max(ans, score);
            }
            
            for (int i = idx; i < N; i++) {
                idx++;
                combination(idx, calorie + burger[i].getK(), score + burger[i].getT());
            }
        }
    }

  
훨씬 간단하게 코드를 짤 수 있다.  
햄버거를 배낭을 넣을때, 넣지 않았을때 2가지의 경우를 재귀해주면 된다.  

CODE2

    static void combination(int idx, int calorie, int score) {
		if (calorie > L) {
			return;
		}
		if(idx == N)
		{
			ans = Math.max(ans, score);
			return;
		}

		combination(idx + 1 , calorie + burger[idx].getK(), score + burger[idx].getT()); // 햄버거를 배낭에 넣을때
		combination(idx + 1 , calorie, score); // 햄버거를 배낭에 안넣을때
	}

        
# 23.01.12(목)
* 자바, 이클립스, SWEA문제 형식에 익숙하지 않아 정말 어이없는 실수를 하여 1시간반이나 시간을 날렸다....
* 익숙해지도록 하자
* C++에서 vector<pair>에 너무 익숙하여 Class 햄버거를 만들었는데 그냥 T, K 배열 2개를 만들어도 괜찮을텐데... 아직 자바로 코테하는게 익숙하지 않아서 그런 것 같다. 