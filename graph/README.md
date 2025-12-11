# Graph

## [순위](https://school.programmers.co.kr/learn/courses/30/lessons/49191)

```
class Solution {
    public int solution(int n, int[][] results) {
        int answer = 0;
        boolean[][] match = new boolean[n+1][n+1]; // graph
        for(int i = 0 ; i < results.length; i++) {
            int u = results[i][0];
            int v = results[i][1];
            match[u][v] = true;
        }
        
        for(int k = 1 ; k <= n ; k++) {
            for(int i = 1; i <= n ; i++) {
                for(int j = 1; j <= n ; j++) {
                    if(match[i][k] && match[k][j]) {
                        match[i][j] = true;
                    }
                }
            }
        }
        
        for(int i = 1; i <= n; i++) {
            int cnt = 0;
            for(int j = 1; j <= n; j++) {
                if(i == j) continue;
                if(match[i][j] || match[j][i]) cnt++;
            }
            
            if(cnt == n-1) answer++;
        }
        
        return answer;
    }
}
```