# Stack

## [주식가격](https://school.programmers.co.kr/learn/courses/30/lessons/42584)

```
import java.util.*;

class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        Stack<Integer> st = new Stack<>(); 
        for(int i = 0 ; i < prices.length; i++) {
            while(!st.isEmpty() && prices[st.peek()] > prices[i]) {
                int top = st.pop();
                answer[top] = i - top; 
            }
            st.push(i);
        }
        while(!st.isEmpty()) {
            int top = st.pop();
            int n = prices.length;
            answer[top] = (n-1) - top;
        }
        return answer;
    }
}
```