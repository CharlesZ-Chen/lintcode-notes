[116. Jump Game](http://www.lintcode.com/problem/jump-game)

- [prev: 115. Unique Paths II](115-unique-paths-ii.md)
- [next: 117. Jump Game II](117-jump-game-ii.md)

---

### DP Version
```java
// keyword: dynamic programming
// time complexity: O(n^2)
// space complexity: O(n)
public class Solution {
    /**
     * @param A: A list of integers
     * @return: The boolean answer
     */
    public boolean canJump(int[] A) {
        if (A == null || A.length < 1) {
            return false;
        }

        boolean[] f = new boolean [A.length];

        f[0] = true;

        for (int i = 1; i < A.length; i++) {
            for (int j = 0; j < i; j++) {
                if (f[j] && A[j] >= i - j) {
                    f[i] = true;
                    break;
                }
            }
        }

        return f[A.length - 1];
    }
}
```

### Greedy Version

```java
// keyword: greedy
// time complexity: O(n)
// space complexity: O(1) in place
public class Solution {
    /**
     * @param A: A list of integers
     * @return: The boolean answer
     */
    public boolean canJump(int[] A) {
        if (A == null || A.length < 1) {
            return false;
        }

        int max = A[0];

        for (int i = 1; i <= max; i++) {
            if (max >= A.length) {
                break;
            }
            else if (A[i] + i > max) {
                max = A[i] + i;
            }
        }

        return max >= A.length - 1;
    }
}
```
---

- [prev: 115. Unique Paths II](115-unique-paths-ii.md)
- [next: 117. Jump Game II](117-jump-game-ii.md)
