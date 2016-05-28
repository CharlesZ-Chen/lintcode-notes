[077. Longest Common Subsequence](http://www.lintcode.com/problem/longest-common-subsequence)

- [prev: 076. Longest Increasing Subsequence](076-longest-increasing-subsequence.md)
- [next: 078. Longest Common Prefix](078-longest-common-prefix.md)

---
#two sequences type DP
Below code implicitly init f[0][...] and f[...][0] to zero.
Basic idea is if we meet equal char at (i + 1, j + 1), then this might contribute to the LCS, thus we let the max([i j] + 1 , [i j+1], [i+1 j]) as the value of ([i+1 j+1]). Otherwise, we let the max([i j], [i j+1], [i+1 j]) as the value of ([i+1 j+1]).

```java
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {
        if (A == null || B == null || A.length() < 1 || B.length() < 1) {
            return 0;
        }

        int lengA = A.length();
        int lengB = B.length();

        // f[i][j] is the LCS of 0 ~ i-1 in A with 0 ~ j-1 in B
        int[][] f = new int [lengA + 1][lengB + 1];

        for (int i = 1; i < lengA + 1; i++) {
            for (int j = 1; j < lengB + 1; j++) {
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    f[i][j] = Math.max(f[i - 1][j - 1] + 1,
                        Math.max(f[i - 1][j], f[i][j - 1]));
                } else {
                    f[i][j] = Math.max(f[i - 1][j - 1],
                        Math.max(f[i - 1][j], f[i][j - 1]));
                }
            }
        }

        return f[lengA][lengB];
    }
}

```

##Little Optimization
If we could have the insight of 1) for each lookup step, at most the LCS would increase by 1; 2) every increase is contribute by some equal char between A and B.
Then we could have the code optimization on line 69 - 70: f[i][j] would be the max(f[i - 1][j], f[i][j - 1]), and only if A.charAt(i - 1) == B.charAt(j - 1), we let f[i][j] directly as f[i - 1][j - 1] + 1.
```java
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {
        if (A == null || B == null || A.length() < 1 || B.length() < 1) {
            return 0;
        }

        int lengA = A.length();
        int lengB = B.length();

        // f[i][j] is the LCS of 0 ~ i-1 in A with 0 ~ j-1 in B
        int[][] f = new int [lengA + 1][lengB + 1];

        for (int i = 1; i < lengA + 1; i++) {
            for (int j = 1; j < lengB + 1; j++) {
                f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + 1;
                }
            }
        }

        return f[lengA][lengB];
    }
}
```

---

- [prev: 076. Longest Increasing Subsequence](076-longest-increasing-subsequence.md)
- [next: 078. Longest Common Prefix](078-longest-common-prefix.md)
