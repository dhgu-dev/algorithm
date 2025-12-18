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

## [정수 삼각형](https://school.programmers.co.kr/learn/courses/30/lessons/43105)

```
import java.util.*;

class Solution {
    public int solution(int[][] triangle) {
        int answer = 0;
        int height = triangle.length;
        int[][] dp = new int[501][501]; // dp[i][j] := i,j 칸에 도달하기 까지 거쳐온 숫자의 최대 합
        
        for(int i = 0 ; i < triangle.length; i++) {
            for(int j = 0 ; j < triangle[i].length; j++) {
                dp[i][j] = triangle[i][j];
            }
        }
        
        for(int i = height-1; i > 0; i--) {
            int width = triangle[i-1].length;
            for(int j = 0 ; j < width; j++) {
                dp[i-1][j] += Math.max(dp[i][j], dp[i][j+1]);
            }
        }
        return dp[0][0];
    }
}
```

## [등굣길](https://school.programmers.co.kr/learn/courses/30/lessons/42898)

```
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        int answer = 0;
        int[][] dp = new int[n+1][m+1]; // dp[i][j] := i,j로 갈 수 있는 최단 경로의 수
        dp[1][1] = 1;
        boolean[][] isPuddle = new boolean[n+1][m+1];
        for(int i = 0 ; i < puddles.length; i++) {
            int x = puddles[i][0];
            int y = puddles[i][1];
            isPuddle[y][x] = true;
        }
        
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if(i == 1 && j == 1) continue;
                if(isPuddle[i][j]) continue;
                dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % 1000000007;
            }
        }
        return dp[n][m] % 1000000007;
    }
}
```