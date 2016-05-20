[068. Binary Tree Postorder Traversal](http://www.lintcode.com/problem/binary-tree-postorder-traversal)

- [prev: 067. Binary Tree Inorder Traversal](067-binary-tree-inorder-traversal.md)
- [next: 069. Binary Tree Level Order Traversal](069-binary-tree-level-order-traversal.md)

---

## Non-Recursion Version

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
     * @return: Postorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> postorderTraversal(TreeNode root) {
        if (root == null) {
            return new ArrayList<Integer> ();
        }
        
        ArrayList<Integer> list = new ArrayList<Integer> ();
        
        Stack<TreeNode> s = new Stack<TreeNode> ();
        Stack<Boolean> visitedS = new Stack<Boolean> ();
        
        s.add(root);
        visitedS.add(false);
        
        while (!s.empty()) {
            boolean visited = visitedS.pop();
            TreeNode visitNode = s.pop();
            if (visited) {
                list.add(visitNode.val);
                continue;
            } else {
                visited = true;
            }

            s.add(visitNode);
            visitedS.add(visited);

            if (visitNode.right != null) {
                s.add(visitNode.right);
                visitedS.add(false);
            }

            if (visitNode.left != null) {
                s.add(visitNode.left);
                visitedS.add(false);
            }
        }
        
        return list;
    }
}
```

---

- [prev: 067. Binary Tree Inorder Traversal](067-binary-tree-inorder-traversal.md)
- [next: 069. Binary Tree Level Order Traversal](069-binary-tree-level-order-traversal.md)
