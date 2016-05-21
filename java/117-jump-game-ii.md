[117. Jump Game II](http://www.lintcode.com/problem/jump-game-ii)

- [prev: 116. Jump Game](116-jump-game.md)
- [next: 118. Distinct Subsequences](118-distinct-subsequences.md)

---
### DP Version
```java
// keyword: dynamic programming
// time complexity: O(n^2)
// space complexity: O(n)
public class Solution {
    /**
     * @param A: A list of lists of integers
     * @return: An integer
     */
    public int jump(int[] A) {
        if (A == null || A.length < 1) {
            return -1;
        }

        // state: f[i] is the minimum steps to reach i position, MAX_VALUE means not reachable
        int[] f = new int [A.length];

        // NOTE: initialize array is a modification operation, thus we cannot use
        // enhanced for-each-loop
        // for (int state : f) {
        //     state = Integer.MAX_VALUE;
        // }
        for (int i = 1; i < f.length; i++) {
            f[i] = Integer.MAX_VALUE;
        }
        f[0] = 0;

        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (f[j] != Integer.MAX_VALUE && A[j] >= i - j) {
                    if (f[i] > f[j] + 1) {
                        f[i] = f[j] + 1;
                    }
                }
            }
        }

        return f[A.length - 1] == Integer.MAX_VALUE ? -1 : f[A.length - 1];
    }
}
```

---

- [prev: 116. Jump Game](116-jump-game.md)
- [next: 118. Distinct Subsequences](118-distinct-subsequences.md)
