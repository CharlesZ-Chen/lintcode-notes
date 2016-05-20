[097. Maximum Depth of Binary Tree](http://www.lintcode.com/problem/maximum-depth-of-binary-tree)

- [prev: 096. Partition List](096-partition-list.md)
- [next: 098. Sort List](098-sort-list.md)

---

Simple application of recursion.

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: An integer.
     */
    public int maxDepth(TreeNode root) {
        // write your code here
        if (root == null) {
            return 0;
        }

        if (root.left == null && root.right == null) {
            return 1;
        }

        int mLleft = maxDepth(root.left);
        int mLright = maxDepth(root.right);
        int mLchild = mLleft > mLright ? mLleft : mLright;

        return 1 +
    }
}
```

---

- [prev: 096. Partition List](096-partition-list.md)
- [next: 098. Sort List](098-sort-list.md)
