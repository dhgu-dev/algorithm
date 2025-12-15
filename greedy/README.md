# Greedy

## [섬 연결하기](https://school.programmers.co.kr/learn/courses/30/lessons/42861)

```
import java.util.*;

class Solution {
    
    int find(int[] parent, int a) {
        if(a == parent[a]) return a;
        return parent[a] = find(parent, parent[a]);
    }
    
    void union(int[] parent, int a, int b) {
        a = find(parent, a);
        b = find(parent, b);
        if (a != b) parent[b] = a;
    }
    
    public int solution(int n, int[][] costs) {
        int answer = 0;
        int[] parent = new int[n];
        for(int i = 0 ; i < n; i++) parent[i] = i;
        
        Arrays.sort(costs, (a, b) -> Integer.compare(a[2], b[2]));
        for(int i = 0 ; i < costs.length; i++) {
            int s = costs[i][0];
            int e = costs[i][1];
            int c = costs[i][2];
            if(find(parent, s) != find(parent, e)) {
                answer += c;
                union(parent, s, e);
            }
        }
        
        return answer;
    }
}
```