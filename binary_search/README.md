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