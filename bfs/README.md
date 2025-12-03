# DFS

## [게임 맵 최단거리](https://school.programmers.co.kr/learn/courses/30/lessons/1844?language=java)

```
import java.util.*;
import java.awt.*; // Point

class Solution {
    public int solution(int[][] maps) {
        int answer = 0;
        int[][] visited = new int[101][101];
        int[] dx = new int[]{1, 0 , -1, 0};
        int[] dy = new int[]{0, 1, 0, -1};
        int n = maps.length;
        int m = maps[0].length;
        int isWall = 0;
        Queue<Point> queue = new LinkedList<>();
        queue.offer(new Point(0,0));
        visited[0][0] = 1;
        
        while(!queue.isEmpty()) {
            Point p = queue.poll();
            if (p.y == n-1 && p.x == m-1) break;
            for(int w = 0 ; w < 4; w++) {
                int x = p.x + dx[w];
                int y = p.y + dy[w];
                if (y < 0 || y >= n || x < 0 || x >= m) continue;
                if(visited[y][x] == 0 && maps[y][x] != isWall) {
                    visited[y][x] = visited[p.y][p.x] + 1;
                    queue.offer(new Point(x, y));
                }
            }
        }
        
        return visited[n-1][m-1] != 0 ? visited[n-1][m-1] : -1;
    }
}
```