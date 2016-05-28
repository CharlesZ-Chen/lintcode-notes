[183. Wood Cut](http://www.lintcode.com/problem/wood-cut)

- [prev: 182. Delete Digits](182-delete-digits.md)
- [next: 184. Largest Number](184-largest-number.md)

---
##One time pass! Wola!

```java
public class Solution {
    /** 
     *@param L: Given n pieces of wood with length L[i]
     *@param k: An integer
     *return: The maximum length of the small pieces.
     */
    public int woodCut(int[] L, int k) {
        if (L == null || k < 0) {
            return 0;
        }

        int maxLen = 0;

        for (int i = 0; i < L.length; i++) {
            assert L[i] >= 0;
            if (L[i] > maxLen) {
                maxLen = L[i];
            }
        }

        int start = 0;
        int end = maxLen;

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int num = _getWoodNumWithLen(mid, L);

            if (num < k) {
                end = mid;
            } else {
                start = mid;
            }
        }

        return _getWoodNumWithLen(end, L) < k ? start : end;
    }

    protected int _getWoodNumWithLen(int len, int[] L) {
        assert L != null && len > 0;

        int num = 0;
        for (int i = 0; i < L.length; i++) {
            num += L[i] / len;
        }

        return num;
    }
}
```

---

- [prev: 182. Delete Digits](182-delete-digits.md)
- [next: 184. Largest Number](184-largest-number.md)
