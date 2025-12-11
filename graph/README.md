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

## [가장 먼 노드](https://school.programmers.co.kr/learn/courses/30/lessons/49189)

```
import java.util.*;

class Solution {
    public int solution(int n, int[][] edge) {
        int longDist = 0;
        int[] dist = new int[n+1];
        boolean[] visited = new boolean[n+1];
        List<Integer>[] graph = new ArrayList[n+1];
        for(int i = 0 ; i <= n ; i++) graph[i] = new ArrayList<>();
        
        for(int i = 0 ; i < edge.length; i++) {
            int u = edge[i][0];
            int v = edge[i][1];
            graph[u].add(v);
            graph[v].add(u);
        }
        
        Queue<Integer> q = new LinkedList<>();
        q.add(1);
        dist[1] = 0;
        visited[1] = true;
        while(!q.isEmpty()) {
            int cur = q.poll();
            for(int adj : graph[cur]) {
                if(!visited[adj]) {
                    visited[adj] = true;
                    q.add(adj);
                    dist[adj] = dist[cur] + 1;
                    longDist = Math.max(longDist, dist[adj]);
                }
            }
        }
        
        int answer = 0 ;
        for(int d : dist) {
            if(d == longDist) answer++;
        }
        
        return answer;
    }
}
```