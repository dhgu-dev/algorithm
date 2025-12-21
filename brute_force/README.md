# Brute Force

## [통학의 신](https://www.acmicpc.net/problem/17945) 

```
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String line = br.readLine();
        
        StringTokenizer st = new StringTokenizer(line);

        int A = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());

        // 근과 계수의 관계에 의거, -1000 <= "두 근의 곱 == B" <= 1000 이므로 완전 탐색이 가능
        for (int x = -1000; x <= 1000; x++) {
            if(x*x + 2*A*x + B == 0) {
                System.out.print(x + " ");
            }
        }
    }
}
```