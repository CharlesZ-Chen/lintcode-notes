[108. Palindrome Partitioning II](http://www.lintcode.com/problem/palindrome-partitioning-ii)

- [prev: 107. Word Break](107-word-break.md)
- [next: 109. Triangle](109-triangle.md)

---

Note: when we need string computation (equalTo, isPlnd ...), think about could we using some extra space to cache the computed result if there were repeated computing happended.
```java
public class Solution {
    /**
     * @param s a string
     * @return an integer
     */
    public int minCut(String s) {
        if (s == null || s.length() < 2) {
            return 0;
        }

        int length = s.length();
        int[][] plndHash = new int [length + 1][length + 1];

        // state: f[i] is the min cuts of subStr 0 ~ i - 1
        int[] f = new int [length + 1];
        for (int i = 0; i < f.length; i++) {
            f[i] = Integer.MAX_VALUE;
        }

        f[0] = -1;
        f[1] = 0;

        for (int i = 2; i < length + 1; i++) {
            for (int j = 0; j < i; j++) {
                if (plndHash[i][j] == 0) {
                    plndHash[i][j] = isPlnd(s.substring(j,i)) ? 1 : -1;
                }
                if (plndHash[i][j] == -1) {
                    continue;
                }

                f[i] = Math.min(f[i], f[j] + 1);
            }
        }

        return f[length];
    }

    public boolean isPlnd(String s) {
        if (s == null) {
            return false;
        }
        if (s.length() < 2) {
            return true;
        }

        for (int i = 0, j = s.length() - 1; i < j; i++, j--) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
        }

        return true;
    }
};
```

---

- [prev: 107. Word Break](107-word-break.md)
- [next: 109. Triangle](109-triangle.md)
