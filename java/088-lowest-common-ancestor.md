[088. Lowest Common Ancestor](http://www.lintcode.com/problem/lowest-common-ancestor)

- [prev: 087. Remove Node in Binary Search Tree](087-remove-node-in-binary-search-tree.md)
- [next: 089. k Sum](089-k-sum.md)

---

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
     * @param root: The root of the binary search tree.
     * @param A and B: two nodes in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null) {
            return null;
        }

        if (root.val == A.val) {
            return A;
        }

        if (root.val == B.val) {
            return B;
        }

        TreeNode left = lowestCommonAncestor(root.left, A, B);

        TreeNode right = lowestCommonAncestor(root.right, A, B);

        if (left != null && right != null) {
            return root;
        }

        if (left == null && right == null) {
            return null;
        }

        if (left == null && right != null) {
            return right;
        } else {
            return left;
        }
    }
}
```

A more concise code:

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
     * @param root: The root of the binary search tree.
     * @param A and B: two nodes in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null || root == A || root == B) {
            return root;
        } 

        TreeNode left = lowestCommonAncestor(root.left, A, B);

        TreeNode right = lowestCommonAncestor(root.right, A, B);

        if (left != null && right != null) {
            return root;
        }

        if (left != null) {
            return left;
        }

        if (right != null) {
            return right;
        }

        return null;
    }
}
```

---

- [prev: 087. Remove Node in Binary Search Tree](087-remove-node-in-binary-search-tree.md)
- [next: 089. k Sum](089-k-sum.md)
