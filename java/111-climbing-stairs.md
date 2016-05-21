[111. Climbing Stairs](http://www.lintcode.com/problem/climbing-stairs)

- [prev: 110. Minimum Path Sum](110-minimum-path-sum.md)
- [next: 112. Remove Duplicates from Sorted List](112-remove-duplicates-from-sorted-list.md)

---

```java
public class Solution {
    /**
     * @param obstacleGrid: A list of lists of integers
     * @return: An integer
     */
    public int uniquePathsWithObstacles(int[][] A) {
        if (A == null || A.length < 1) {
            return -1;
        }

        int m = A.length;
        int n = A[0].length;

        int[][] f = new int [2][n];

        boolean isBlockVer = false;
        boolean isBlockHor = false;

        if (A[0][0] == 1) {
            return 0;
        }

        for (int j  = 0; j < n; j++) {
            if (isBlockHor) {
                f[0][j] = 0;
            } else if (A[0][j] == 1) {
                isBlockHor = true;
                f[0][j] = 0;
            } else {
                f[0][j] = 1;
            }
        }
        if (m > 1) {
            if (A[1][0] == 1) {
                isBlockVer = true;
                f[1][0] = 0;
            } else {
                f[1][0] = 1;
            }
        }

        for (int i = 1; i < m; i++) {
            if (isBlockVer) {
                f[i % 2][0] = 0;
            } else if (A[i][0] == 1) {
                isBlockVer = true;
                f[i % 2][0] = 0;
            } else {
                f[i % 2][0] = 1;
            }
            for (int j = 1; j < n; j++) {
                f[i % 2][j] = A[i][j] == 1 ? 0 : f[i % 2][j - 1] + f[(i - 1) % 2][j];
            }
        }

        return f[(m - 1) % 2][n - 1];
    }
}
```

---

- [prev: 110. Minimum Path Sum](110-minimum-path-sum.md)
- [next: 112. Remove Duplicates from Sorted List](112-remove-duplicates-from-sorted-list.md)
