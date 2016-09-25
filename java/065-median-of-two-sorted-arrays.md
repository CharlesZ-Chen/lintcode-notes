[065. Median of two Sorted Arrays](http://www.lintcode.com/problem/median-of-two-sorted-arrays)

- [prev: 064. Merge Sorted Array](064-merge-sorted-array.md)
- [next: 066. Binary Tree Preorder Traversal](066-binary-tree-preorder-traversal.md)

---

Each time we drop k/2 elements, and narrow down the problem to find k/2 th element in the new scope.

```java
class Solution {
    /**
     * @param A: An integer array.
     * @param B: An integer array.
     * @return: a double whose format is *.5 or *.0
     */
    public double findMedianSortedArrays(int[] A, int[] B) {
        if (A == null || B == null) {
            return -1;
        }

        int num = A.length + B.length;

        if (num % 2 == 1) {
            return getKthNumber(num / 2 + 1, A, 0, B, 0);
        } else {
            return (getKthNumber(num / 2, A, 0, B, 0) +
                getKthNumber(num / 2 + 1, A, 0, B, 0)) / 2.0;
        }
    }

    public double getKthNumber(int k, int[] A, int A_start, int[] B, int B_start) {
        if (A_start >= A.length) {
            return B[B_start + k - 1];
        }

        if (B_start >= B.length) {
            return A[A_start + k - 1];
        }

        if ( k == 1) {
            return Math.min(A[A_start], B[B_start]);
        }

        int A_key = A_start + k / 2 - 1 < A.length ?
            A[A_start + k / 2 - 1] : Integer.MAX_VALUE;

        int B_key = B_start + k / 2 - 1 < B.length ?
            B[B_start + k / 2 - 1] : Integer.MAX_VALUE;

        if (A_key > B_key) {
            return getKthNumber(k - k / 2, A, A_start, B, B_start + k /2);
        } else {
            return getKthNumber(k - k / 2, A, A_start + k / 2, B, B_start);
        }
    }
}

```

---

- [prev: 064. Merge Sorted Array](064-merge-sorted-array.md)
- [next: 066. Binary Tree Preorder Traversal](066-binary-tree-preorder-traversal.md)
