# Brute Force

## [통학의 신](https://www.acmicpc.net/problem/17945)

```java
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

## [Farm](https://www.acmicpc.net/problem/16283)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String line = br.readLine();
        
        StringTokenizer st = new StringTokenizer(line);

        int A = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());
        int N = Integer.parseInt(st.nextToken());
        int W = Integer.parseInt(st.nextToken());

        String result = "";
        for (int x = 1; x < N; x++) {
            int cost = x * A + (N - x) * B;
            if (cost == W) {
                if (!result.equals("")) {
                    System.out.print(-1);
                    return;
                }
                result = x + " " + (N - x);
            }
        }

        if (result.equals("")) {
            System.out.print(-1);
            return;
        }

        System.out.print(result);
    }
}
```

## [일곱 난쟁이](https://www.acmicpc.net/problem/2309)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int[] arr = new int[9];
        int sum = 0;
        for (int i = 0; i < 9; i++) {
            String line = br.readLine();
            arr[i] = Integer.parseInt(line);
            sum += arr[i];
        }

        Arrays.sort(arr);

        for (int i = 0; i < 9; i++) {
            for(int j = i+1; j < 9; j++) {
                if (sum - arr[i] - arr[j] == 100) {
                    for (int k = 0 ; k < 9; k++) {
                        if (k == i || k == j) continue;
                        System.out.println(arr[k]);
                    }
                    return;
                }
            }
        }
    }
}
```

## [2017 연세대학교 프로그래밍 경시대회](https://www.acmicpc.net/problem/14568)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line = br.readLine();
        int N = Integer.parseInt(line);

        int cnt = 0;
        for (int i = 1; i < N; i++) {
            if (i % 2 != 0) continue;
            for (int j = 1; j < N; j++) {
                if (N - i - j <= 0) continue;
                if (j + 2 <= N - i - j) {
                    cnt++;
                }
            }
        }

        System.out.println(cnt);
    }
}
```

## [완전 제곱수](https://www.acmicpc.net/problem/6131)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line = br.readLine();
        int N = Integer.parseInt(line);

        int cnt = 0;
        for (int a = 1; a <= 500; a++) {
            for (int b = 1; b <= 500; b++) {
                if (a * a == b * b + N) {
                    cnt++;
                }
            }
        }

        System.out.println(cnt);
    }
}
```

## [대회 or 인턴](https://www.acmicpc.net/problem/2875)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line = br.readLine();
        StringTokenizer st = new StringTokenizer(line);

        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int K = Integer.parseInt(st.nextToken());

        int ans = 0;
        for (int i = 0; i <= K; i++) {
            int female = N - i;
            int male = M - (K - i);
            if (female <= 0 || male <= 0) continue; 
            int teams = Math.min(female / 2, male);
            ans = Math.max(ans, teams);
        }

        System.out.println(ans);
    }
}
```

## [슈퍼 마리오](https://www.acmicpc.net/problem/2851)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int[] arr = new int[11];
        
        for (int i = 0; i < 10; i++) {
            String line = br.readLine();
            arr[i] = Integer.parseInt(line);
        }

        int ans = 0;
        for (int i = 1; i <= 10; i++) {
            int score = 0;
            for(int j = 0; j < i; j++) {
                score += arr[j];
            }
            int cur = Math.abs(100 - score);
            int prev = Math.abs(100 - ans);
            if (cur <= prev) ans = score;
        }
        System.out.println(ans);
    }
}
```

## [방 배정하기](https://www.acmicpc.net/problem/14697)

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String line = br.readLine();
        StringTokenizer st = new StringTokenizer(line);

        int A = Integer.parseInt(st.nextToken());
        int B = Integer.parseInt(st.nextToken());
        int C = Integer.parseInt(st.nextToken());
        int N = Integer.parseInt(st.nextToken());

        int ans = 0;
        
        for (int i = 0 ; i <= N ; i++) {
            for (int j = 0 ; j <= N ; j++) {
                for (int k = 0 ; k <= N ; k++) {
                    if (i * A + j * B + k * C != N) continue;
                    ans = 1;
                }
            }
        }

        System.out.println(ans);
    }
}
```