[118. Distinct Subsequences](http://www.lintcode.com/problem/distinct-subsequences)

- [prev: 117. Jump Game II](117-jump-game-ii.md)
- [next: 119. Edit Distance](119-edit-distance.md)

---

The state is easy to come out, the real hard part is the tranfser function: 
```
 if (T.charAt(i - 1) == S.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + f[i][j - 1];
                } else {
                    f[i][j] = f[i][j - 1]; // just successor the previous count
                }
```

It needs us to really clear with the concept of **sequence**. Because we only need to keep the order of matching chars, thus we can add up all previous f[i - 1][j - 1] if T[i - 1] == S[j -1].

**Think about what the transfer function will be if we ask for subString rather than subSequence.**

```java
public class Solution {
    /**
     * @param S, T: Two string.
     * @return: Count the number of distinct subsequences
     */
    public int numDistinct(String S, String T) {
        if (S == null || T == null ||
            S.length() < T.length()) {
            return 0;
        }

        int lengS = S.length();
        int lengT = T.length();

        // state: f[i][j] is the max num of dist_subS of 0 ~ i -1 of T in 0 ~ j -1 S
        int[][] f = new int [lengT + 1][lengS + 1];

        for (int i = 1; i < lengT + 1; i++) {
            f[i][0] = 0; // non-empty T has zero subS in empty S
        }
        for (int j = 1; j < lengS + 1; j++) {
            f[0][j] = 1; // empty T has one subS in non-empty S
        }
        f[0][0] = 1; // empty T has one subS in empty S

        for (int i = 1; i < lengT + 1; i++) {
            for (int j = 1; j < lengS + 1; j++) {
                if (i > j) {
                    f[i][j] = 0; // lengT > lengS, thus has non subS of T in S
                    continue;
                }

                if (T.charAt(i - 1) == S.charAt(j - 1)) {
                    f[i][j] = f[i - 1][j - 1] + f[i][j - 1]; 
                        // the subS in j -1 contribute to i,j with f[i - 1][j - 1] because all subS - 1 could become a subS with the end char.
                } else {
                    f[i][j] = f[i][j - 1]; // just successor the previous count
                }
            }
        }

        return f[lengT][lengS];
    }
}
```

---

- [prev: 117. Jump Game II](117-jump-game-ii.md)
- [next: 119. Edit Distance](119-edit-distance.md)
