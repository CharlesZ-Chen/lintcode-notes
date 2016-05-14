[066. Binary Tree Preorder Traversal](http://www.lintcode.com/problem/binary-tree-preorder-traversal)

- [prev: 065. Median of two Sorted Arrays](065-median-of-two-sorted-arrays.md)
- [next: 067. Binary Tree Inorder Traversal](067-binary-tree-inorder-traversal.md)

---

## Recursion version
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
     * @return: Preorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> preorderTraversal(TreeNode root) {

        ArrayList<Integer> list = new ArrayList<Integer> ();
        preorderHelper(list, root);

        return list;
    }
    
    public void preorderHelper(ArrayList<Integer> list, TreeNode root) {
        if(root == null) {
            return;
        }
        list.add(root.val);
        preorderHelper(list, root.left);
        preorderHelper(list, root.right);
    }
}
```

## Non-recursive version

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
     * @return: Preorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        if (root == null) {
            return new ArrayList<Integer> ();
        }

        ArrayList<Integer> list = new ArrayList<Integer> ();

        Stack<TreeNode> s = new Stack<TreeNode> ();

        s.add(root);

        while (!s.empty()) {
            TreeNode visitNode = s.pop();
            list.add(visitNode.val);

            if (visitNode.right != null) {
                s.add(visitNode.right);
            }

            if (visitNode.left != null) {
                s.add(visitNode.left);
            }
        }

        return list;
    }
}
```

---

- [prev: 065. Median of two Sorted Arrays](065-median-of-two-sorted-arrays.md)
- [next: 067. Binary Tree Inorder Traversal](067-binary-tree-inorder-traversal.md)
