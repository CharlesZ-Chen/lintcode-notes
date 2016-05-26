[119. Edit Distance](http://www.lintcode.com/problem/edit-distance)

- [prev: 118. Distinct Subsequences](118-distinct-subsequences.md)
- [next: 120. Word Ladder](120-word-ladder.md)

---
## Two sequences type DP
```java
public class Solution {
    /**
     * @param word1 & word2: Two string.
     * @return: The minimum number of steps.
     */
    public int minDistance(String word1, String word2) {
        if (word1 == null || word2 == null) {
                return 0;
            }

        int leng_A = word1.length();
        int leng_B = word2.length();

        // state: f[i][j] is the min edit 
        // between 0 ~ i - 1 in word1 and 0~ j - 1 in word2
        int[][] f = new int[leng_A + 1][leng_B + 1];

        for (int i = 0; i < leng_A + 1; i++) {
            f[i][0] = i;
        }

        for (int j = 0; j < leng_B + 1; j++) {
            f[0][j] = j;
        }

        for (int i = 1; i < leng_A + 1; i++) {
            for (int j = 1; j < leng_B + 1; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    f[i][j] = Math.min(f[i -1][j - 1], 
                        Math.min(f[i][j - 1] + 1, f[i - 1][j] + 1));
                } else {
                    f[i][j] = Math.min(f[i - 1][j - 1] + 1,
                        Math.min(f[i][j - 1] + 1, f[i - 1][j] + 1));
                }
            }
        }

        return f[leng_A][leng_B];
    }
}
```
## Little Optimization on computing f[i][j]

```java
public class Solution {
    /**
     * @param word1 & word2: Two string.
     * @return: The minimum number of steps.
     */
    public int minDistance(String word1, String word2) {
        if (word1 == null || word2 == null) {
                return 0;
            }

        int leng_A = word1.length();
        int leng_B = word2.length();

        // state: f[i][j] is the min edit 
        // between 0 ~ i - 1 in word1 and 0~ j - 1 in word2
        int[][] f = new int[leng_A + 1][leng_B + 1];

        for (int i = 0; i < leng_A + 1; i++) {
            f[i][0] = i;
        }

        for (int j = 0; j < leng_B + 1; j++) {
            f[0][j] = j;
        }

        for (int i = 1; i < leng_A + 1; i++) {
            for (int j = 1; j < leng_B + 1; j++) {
                f[i][j] = 1 + Math.min(f[i - 1][j - 1],
                        Math.min(f[i][j - 1], f[i - 1][j]));
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    f[i][j] = f[i -1][j - 1];
                } 
            }
        }

        return f[leng_A][leng_B];
    }
}
```
---

- [prev: 118. Distinct Subsequences](118-distinct-subsequences.md)
- [next: 120. Word Ladder](120-word-ladder.md)
