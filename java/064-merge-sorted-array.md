[064. Merge Sorted Array](http://www.lintcode.com/problem/merge-sorted-array)

- [prev: 063. Search in Rotated Sorted Array II](063-search-in-rotated-sorted-array-ii.md)
- [next: 065. Median of two Sorted Arrays](065-median-of-two-sorted-arrays.md)

---

Simple array operation.

```java
class Solution {
    /**
     * @param A: sorted integer array A which has m elements, 
     *           but size of A is m+n
     * @param B: sorted integer array B which has n elements
     * @return: void
     */
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        if (A == null || B == null || A.length < B.length || A.length == 0) {
            return;
        }

        int k = m + n - 1;
        int i = m - 1;
        int j = n - 1;

        while (j > -1) {
           if (i > -1 && A[i] > B[j]) {
               A[k--] = A[i--];
           } else {
               A[k--] = B[j--];
           }
        }
    }
}
```

---

- [prev: 063. Search in Rotated Sorted Array II](063-search-in-rotated-sorted-array-ii.md)
- [next: 065. Median of two Sorted Arrays](065-median-of-two-sorted-arrays.md)
