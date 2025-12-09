# Binary Search

## [입국 심사](https://school.programmers.co.kr/learn/courses/30/lessons/43238)

```
class Solution {
    boolean check(long target, long n, int[] times) {
        long sum = 0;
        for(int time : times) {
            if(target < time) continue;
            sum += (target / time);
        }
        if(n <= sum) return true;
        return false;
    }

    public long solution(int n, int[] times) {
        long left = 1, right = (long)1e9 * n;
        long answer = right;
        while(left <= right) {
            long mid = (left + right) / 2;
            if(check(mid, n, times)) {
                answer = Math.min(answer, mid);
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return answer;
    }
}
```

## [징검다리](https://school.programmers.co.kr/learn/courses/30/lessons/43236)

```
import java.util.*;
import java.util.stream.*;

class Solution {
    public int solution(int distance, int[] rocks, int n) {
        int answer = 0;
        List<Integer> pos = Arrays.stream(rocks).boxed().collect(Collectors.toList());
        Collections.sort(pos);
        pos.add(distance);
        
        long s = 0, e = distance;
        while(s <= e) {
            long minDist = (s + e) / 2;
            long prev = 0;
            int removedRock = 0;
            for(int rock : pos) {
                if(rock - prev < minDist) {
                    removedRock += 1;
                } else {
                    prev = rock;   
                }
            }
            if(removedRock > n) {
                e = minDist - 1;
            } else {
                answer = Math.max(answer, (int)minDist);
                s = minDist + 1;
            }
        }
        return answer;
    }
}
```