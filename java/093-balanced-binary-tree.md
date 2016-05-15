[093. Balanced Binary Tree](http://www.lintcode.com/problem/balanced-binary-tree)

- [prev: 092. Backpack](092-backpack.md)
- [next: 094. Binary Tree Maximum Path Sum](094-binary-tree-maximum-path-sum.md)

---
## naive version

using condition: if a BT is balanced, then: BT.left.isBalanced && BT.right.isBalanced && abs(BT.left.maxLength - BT.right.maxLength) <= 1

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
http://www.lintcode.com/en/problem/balanced-binary-tree/#     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }

        if (root.left == null && root.right == null) {
            return true;
        }

        return isBalanced(root.left) && isBalanced(root.right) &&
            Math.abs(maxDepth(root.left) - maxDepth(root.right)) <= 1;
    }

    public int maxDepth(TreeNode root) {
        if ( root == null) {
            return 0;
        }

        if (root.left == null && root.right == null) {
            return 1;
        }

        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```
## Using -1 propogate length and isBalanced information

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
http://www.lintcode.com/en/problem/balanced-binary-tree/#     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        
        if (root.left == null && root.right == null) {
            return true;
        }
        
        return maxDepth(root) != -1;
    }
    
    public int maxDepth(TreeNode root) {
        if ( root == null) {
            return 0;
        }
        
        if (root.left == null && root.right == null) {
            return 1;
        }
        
        int leftMaxDepth = maxDepth(root.left);
        int rightMaxDepth = maxDepth(root.right);
        
        if (leftMaxDepth == -1 || rightMaxDepth == -1 ||
            Math.abs(leftMaxDepth - rightMaxDepth) > 1) {
           return -1;  
        }
        
        return Math.max(leftMaxDepth, rightMaxDepth) + 1;
    }
}
```
---

- [prev: 092. Backpack](092-backpack.md)
- [next: 094. Binary Tree Maximum Path Sum](094-binary-tree-maximum-path-sum.md)
