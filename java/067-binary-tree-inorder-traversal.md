[067. Binary Tree Inorder Traversal](http://www.lintcode.com/problem/binary-tree-inorder-traversal)

- [prev: 066. Binary Tree Preorder Traversal](066-binary-tree-preorder-traversal.md)
- [next: 068. Binary Tree Postorder Traversal](068-binary-tree-postorder-traversal.md)

---

## Non-Recursive Veraion

```java
// keyword: Binary Tree, Inorder Traversal
// time complexity: O(n)
// space complexity: O(n)
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
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        if (root == null) {
            return new ArrayList<Integer> ();
        }

        ArrayList<Integer> list = new ArrayList<Integer> ();

        Stack<TreeNode> s = new Stack<TreeNode> ();
        Stack<Boolean> visitS = new Stack<Boolean> ();
        
        s.add(root);
        visitS.add(false);

        while (!s.empty()) {
            TreeNode visitNode = s.pop();
            boolean isVisited = visitS.pop();
            if (isVisited) {
                list.add(visitNode.val);
                continue;
            }
            isVisited = true;

            if (visitNode.right != null) {
                s.add(visitNode.right);
                visitS.add(false);
            }

            s.add(visitNode);
            visitS.add(isVisited);

            if (visitNode.left != null) {
                s.add(visitNode.left);
                visitS.add(false);
            } 
        }

        return list;
    }
}
```

## A more efficient Non-Recursive Version that save the extra O(n) space of boolean stack

```java
// keyword: binary tree, inorder traversal
// time complexity: O(n)
// space complexity: O(n)
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
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        if (root == null) {
            return new ArrayList<Integer> ();
        }

        ArrayList<Integer> list = new ArrayList<Integer> ();
        Stack<TreeNode> s = new Stack<TreeNode> ();

        TreeNode curt = root;

        while (curt != null || !s.empty()) {
            while (curt != null) {
                s.add(curt);
                curt = curt.left;
            }
            curt = s.pop();
            list.add(curt.val);
            curt = curt.right;
        }

        return list;
    }
}
```


---

- [prev: 066. Binary Tree Preorder Traversal](066-binary-tree-preorder-traversal.md)
- [next: 068. Binary Tree Postorder Traversal](068-binary-tree-postorder-traversal.md)
