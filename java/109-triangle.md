[109. Triangle](http://www.lintcode.com/problem/triangle)

- [prev: 108. Palindrome Partitioning II](108-palindrome-partitioning-ii.md)
- [next: 110. Minimum Path Sum](110-minimum-path-sum.md)

---

```java
public class Solution {
    public boolean[] visited;
    public int[] cache;
    /**
     * @param triangle: a list of lists of integers.
     * @return: An integer, minimum path sum.
     */
    public int minimumTotal(int[][] triangle) {
        if (triangle == null || triangle.length < 1) {
            return 0;
        }

        int n = triangle.length;
        visited = new boolean [((1+n) * n) / 2];
        cache = new int [((1+n) * n) / 2];

        int min = helper(triangle, 0, 0);
        return min;
    }

    public int helper(int[][] tri, int pos_col, int level) {
        assert pos_col < tri[level].length;

        if (level == tri.length - 1) {
            return tri[level][pos_col];
        }

        int idx = (level * (level + 1)) / 2 + pos_col;
        if (visited[idx]) {
            return cache[idx];
        }

        int left = helper(tri, pos_col, level + 1);
        int right = helper(tri, pos_col + 1, level + 1);

        int min = tri[level][pos_col] + Math.min(left, right);
        visited[idx] = true;
        cache[idx] = min;
        return min;
    }
}
```

---

- [prev: 108. Palindrome Partitioning II](108-palindrome-partitioning-ii.md)
- [next: 110. Minimum Path Sum](110-minimum-path-sum.md)
