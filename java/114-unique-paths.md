[114. Unique Paths](http://www.lintcode.com/problem/unique-paths)

- [prev: 113. Remove Duplicates from Sorted List II](113-remove-duplicates-from-sorted-list-ii.md)
- [next: 115. Unique Paths II](115-unique-paths-ii.md)

---

```java
public class Solution {
    /**
     * @param grid: a list of lists of integers.
     * @return: An integer, minimizes the sum of all numbers along its path
     */
    public int minPathSum(int[][] grid) {
        if (grid == null || grid.length < 1) {
            return -1;
        }

        int m = grid.length;
        int n = grid[0].length;

        int[][] f = new int [m][n];
        
        f[0][0] = grid[0][0];
        
        //initialize
        for (int i = 1; i < m; i++) {
            f[i][0] = f[i - 1][0] + grid[i][0];
        }
        for (int j = 1; j < n; j++) {
            f[0][j] = f[0][j - 1] + grid[0][j];
        }

        //top - down
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                f[i][j] = grid[i][j] + Math.min(f[i - 1][j], f[i][j-1]);
            }
        }

        return f[m - 1][n - 1];
    }
}

```

---

- [prev: 113. Remove Duplicates from Sorted List II](113-remove-duplicates-from-sorted-list-ii.md)
- [next: 115. Unique Paths II](115-unique-paths-ii.md)
