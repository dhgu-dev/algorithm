# Heap

## [디스크 컨트롤러](https://school.programmers.co.kr/learn/courses/30/lessons/42627)

```
import java.util.*;
import java.util.stream.*;

class Solution {
    
    class Task implements Comparable<Task> {
        int id;
        int reqAt;
        int cost;
        
        public Task(int id, int reqAt, int cost) {
            this.id = id;
            this.reqAt = reqAt;
            this.cost = cost;
        }
        
        @Override
        public int compareTo(Task o) {
            if(this.cost == o.cost) {
                if(this.reqAt == o.reqAt) {
                    return Integer.compare(this.id, o.id);        
                }
                return Integer.compare(this.reqAt, o.reqAt);
            }
            return Integer.compare(this.cost, o.cost);
        }
    }
    
    public int solution(int[][] jobs) {
        int total = 0;
        int curTime = 0;
        int t = 0;
        PriorityQueue<Task> pq = new PriorityQueue<>();
        List<Task> remains = new ArrayList<>();
        for(int i = 0 ; i < jobs.length; i++) {
            int reqAt = jobs[i][0];
            int cost = jobs[i][1];
            remains.add(new Task(i, reqAt, cost));
        }
        Collections.sort(remains, (a, b) -> Integer.compare(a.reqAt, b.reqAt));
        while(t < jobs.length) {
            if(remains.get(t).reqAt <= curTime) {
                Task task = remains.get(t);
                pq.add(task);
                t++;
                continue;
            }
            if(!pq.isEmpty()) {
                Task doTask = pq.poll();
                curTime += doTask.cost;
                total += curTime - doTask.reqAt;
            }
            else {
                curTime = remains.get(t).reqAt;
            }
        }
        while(!pq.isEmpty()) {
            Task doTask = pq.poll();
            curTime += doTask.cost;
            total += curTime - doTask.reqAt;
        }
        return (int)(total / jobs.length);
    }
}
```

## [이중우선순위큐](https://school.programmers.co.kr/learn/courses/30/lessons/42628)

```
import java.util.*;

class Solution {
    public int[] solution(String[] operations) {
        PriorityQueue<Integer> minpq = new PriorityQueue<>();
        PriorityQueue<Integer> maxpq = new PriorityQueue<>(Collections.reverseOrder());
        
        for(String op : operations) {
            if(op.startsWith("I ")) {
                int n = Integer.parseInt(op.substring(2));
                minpq.add(n);
                maxpq.add(n);
            } else if(!minpq.isEmpty() && op.equals("D -1")) {
                maxpq.remove(minpq.poll());
            } else if(!maxpq.isEmpty() && op.equals("D 1")) {
                minpq.remove(maxpq.poll());
            }
        }
        
        if(minpq.isEmpty() && maxpq.isEmpty()) {
            return new int[]{0, 0};
        }
        return new int[]{ maxpq.poll(), minpq.poll() };
    }
}
```