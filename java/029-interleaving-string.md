[029. Interleaving String](http://www.lintcode.com/problem/interleaving-string)

- [prev: 028. Search a 2D Matrix](028-search-a-2d-matrix.md)
- [next: 030. Insert Interval](030-insert-interval.md)

---
##One time pass! Wola!

Be careful to think about the transfer function and state, then this one will be ease:)

```java
public class Solution {
    /**
     * Determine whether s3 is formed by interleaving of s1 and s2.
     * @param s1, s2, s3: As description.
     * @return: true or false.
     */
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1 == null || s2 == null || s3 == null ||
            s1.length() + s2.length() != s3.length()) {
            return false;
        }

        int lenS1 = s1.length();
        int lenS2 = s2.length();
        int lenS3 = s3.length();

        // state: f[i][j] is 0 ~ i-1 in s1 and 0 ~ j - 1in s2 could form 0 ~ i-1+j-1 in s3
        boolean[][] f = new boolean [lenS1 + 1][lenS2 + 1];

        // if s2 is empty, then s1 should be exact same as s3
        for (int i = 1; i < lenS1 + 1; i++) {
            if (s1.charAt(i - 1) != s3.charAt(i - 1)) {
                break;
            }
            f[i][0] = true;
        }

        // if s1 is empty, then s2 should be exact same as s3
        for (int j = 1; j < lenS2 + 1; j++) {
            if (s2.charAt(j - 1) != s3.charAt(j - 1)) {
                break;
            }
            f[0][j] = true;
        }

        // if s1 and s2 both empty, then it is ture with our state definition.
        f[0][0] = true;

        for (int i = 1; i < lenS1 + 1; i++) {
            for (int j = 1; j < lenS2 + 1; j++) {
                int tail = i + j - 1;
                if (!f[i - 1][j] && !f[i][j - 1]) {
                    f[i][j] = false;
                }
                else if (!f[i - 1][j] && f[i][j - 1]) {
                    f[i][j] = s2.charAt(j - 1) == s3.charAt(tail);
                }
                else if (f[i - 1][j] && !f[i][j -1]) {
                    f[i][j] = s1.charAt(i - 1) == s3.charAt(tail);
                }
                else if (f[i - 1][j] && f[i][j - 1]) {
                    f[i][j] = s1.charAt(i - 1) == s3.charAt(tail) ||
                        s2.charAt(j - 1) == s3.charAt(tail);
                } else {
                    assert false;
                }
            }
        }

        return f[lenS1][lenS2];
    }
}
```
---

- [prev: 028. Search a 2D Matrix](028-search-a-2d-matrix.md)
- [next: 030. Insert Interval](030-insert-interval.md)
