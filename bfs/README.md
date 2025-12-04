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

## [아이템 줍기](https://school.programmers.co.kr/learn/courses/30/lessons/87694)

```
import java.util.*;
import java.awt.*;

class Solution {
    public int solution(int[][] rectangle, int characterX, int characterY, int itemX, int itemY) {
        int answer = 0;
        int cnt = rectangle.length;
        int[][] maps = new int[101][101];
        
        for(int i = 0 ; i < cnt; i++) {
            int[] rect = rectangle[i];
            int x1 = rect[0] * 2;
            int y1 = rect[1] * 2;
            int x2 = rect[2] * 2;
            int y2 = rect[3] * 2;
            
            for(int yy = y1; yy <= y2; yy++) {
                if(yy == y1 || yy == y2) {
                    for(int xx = x1; xx <= x2; xx++) {
                        maps[yy][xx] = 1;
                    }
                }
                else {
                    maps[yy][x1] = 1;
                    maps[yy][x2] = 1;
                }
            }
        }
        
        for(int i = 0 ; i < cnt; i++) {
            int[] rect = rectangle[i];
            int x1 = rect[0] * 2 + 1;
            int y1 = rect[1] * 2 + 1;
            int x2 = rect[2] * 2 - 1;
            int y2 = rect[3] * 2 - 1;
            
            for(int yy = y1; yy <= y2; yy++) {
                for(int xx = x1; xx <= x2; xx++) {
                    maps[yy][xx] = 0;
                }
            }
        }
        
        int[][] dist = new int[101][101];
        Queue<Point> q = new LinkedList<>();
        int[] dx = new int[]{1,0,-1,0};
        int[] dy = new int[]{0,1,0,-1};
        q.offer(new Point(characterX * 2, characterY * 2));
        dist[characterY * 2][characterX * 2] = 1;
        
        while(!q.isEmpty()) {
            Point p = q.poll();
            int x = p.x;
            int y = p.y;
            int d = dist[y][x];
            
            if(y == itemY * 2 && x == itemX * 2) {
                answer = (d-1) / 2;
                break;
            }
            
            for(int w = 0 ; w < 4; w++) {
                int xx = x + dx[w];
                int yy = y + dy[w];
                if(yy < 0 || yy > 100 || xx < 0 || xx > 100) continue;
                if(maps[yy][xx] == 1 && dist[yy][xx] == 0) {
                    q.offer(new Point(xx, yy));
                    dist[yy][xx] = d + 1;
                }
            }
        }
        
        return answer;
    }
}
```