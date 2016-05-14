[155. Minimum Depth of Binary Tree](http://www.lintcode.com/problem/minimum-depth-of-binary-tree)

- [prev: 154. Regular Expression Matching](154-regular-expression-matching.md)
- [next: 156. Merge Intervals](156-merge-intervals.md)

---

Only need to notice one thing: the definition of `leaf` is a `node` has no `chlidren`. See [Tree Terminologies](https://en.wikipedia.org/wiki/Tree_(data_structure)#Terminologies_used_in_Trees)

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
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        return minDepthHelper(root);
    }

    public int minDepthHelper(TreeNode root) {
        if (root == null) {
            return Integer.MAX_VALUE;
        }

        if (root.left == null && root.right == null) {
            return 1;
        }

        return Math.min(minDepthHelper(root.right), minDepthHelper(root.left)) + 1;
    }
}
```

---

- [prev: 154. Regular Expression Matching](154-regular-expression-matching.md)
- [next: 156. Merge Intervals](156-merge-intervals.md)
