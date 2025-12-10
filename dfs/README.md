# DFS

## [피로도](https://school.programmers.co.kr/learn/courses/30/lessons/87946)

```
class Solution {
    public int solution(int k, int[][] dungeons) {
        int answer = -1;
        int[] visited = new int[9];
        answer = solve(k, dungeons, visited, 0);
        return answer;
    }
    
    public int solve(int k, int[][] dungeons, int[] visited, int result) {
        if(k <= 0) return result;
        
        int ans = result;
        for(int i = 0 ; i < dungeons.length; i++) {
            int required = dungeons[i][0];
            int cost = dungeons[i][1];
            
            if(required <= k && visited[i] == 0) {
                visited[i] = 1;
                k -= cost;
                int cnt = solve(k, dungeons, visited, result + 1);
                if (cnt > ans) ans = cnt;
                visited[i] = 0;
                k += cost;
            }
        }
        
        return ans;
    }
}
```

## [네트워크](https://school.programmers.co.kr/learn/courses/30/lessons/43162)

```
class Solution {
    
    boolean[] visited = new boolean[201];
    
    public int solution(int n, int[][] computers) {
        int answer = 0;
        
        for(int i = 0 ; i < n; i++) {
            if(!visited[i]) {
                solve(i, n, computers);
                answer++;
            }
        }
        
        return answer;
    }
    
    public void solve(int node, int n, int[][] computers) {
        visited[node] = true;
        
        for(int nxt = 0; nxt < n; nxt++) {
            if(computers[node][nxt] == 1 && !visited[nxt]) {
                solve(nxt, n, computers);
            }
        }
    }
}
```