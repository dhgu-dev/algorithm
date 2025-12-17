# Queue

## [다리를 지나는 트럭](https://school.programmers.co.kr/learn/courses/30/lessons/42583)

```
import java.util.*;
import java.util.stream.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 0;
        int curWeight = 0;
        Queue<Integer> q = new LinkedList<>();
        Queue<Integer> remainTrucks = new LinkedList<>();
        IntStream.range(0, bridge_length).forEach(i -> q.add(0));
        IntStream.range(0, truck_weights.length).forEach(i -> remainTrucks.add(truck_weights[i]));
        while(!remainTrucks.isEmpty()) {
            curWeight -= q.poll();
            if(curWeight + remainTrucks.peek() <= weight) {
                int truck = remainTrucks.poll();
                curWeight += truck;
                q.add(truck);
            }
            else {
                q.add(0);
            }
            answer += 1;
        }
        answer += bridge_length;
        return answer;
    }
}
```