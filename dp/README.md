# Dynamic Programming

## [N으로 표현](https://school.programmers.co.kr/learn/courses/30/lessons/42895)

```
import java.util.*;

class Solution {
    public int solution(int N, int number) {
        Set<Integer> dp[] = new HashSet[9]; // dp[i] := N을 i번 사용해서 만들 수 있는 숫자들의 세트
        for(int i = 0 ; i <= 8; i++) dp[i] = new HashSet<>();
        
        for(int i = 1; i <= 8; i++) {
            int Ns = N;
            for(int j = 1 ; j < i; j++) Ns = 10 * Ns + N;
            dp[i].add(Ns);
            for(int j = 1 ; j <= i; j++) {
                for(int x : dp[j]) {
                    for(int y : dp[i-j]) {
                        dp[i].add(x + y);
                        dp[i].add(x - y);
                        dp[i].add(x * y);
                        if(y != 0) dp[i].add(x / y);
                    }
                }
            }
            if(dp[i].contains(number)) return i;
        }
        
        return -1;
    }
}
```