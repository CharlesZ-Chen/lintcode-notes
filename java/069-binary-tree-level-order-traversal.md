[069. Binary Tree Level Order Traversal](http://www.lintcode.com/problem/binary-tree-level-order-traversal)

- [prev: 068. Binary Tree Postorder Traversal](068-binary-tree-postorder-traversal.md)
- [next: 070. Binary Tree Level Order Traversal II](070-binary-tree-level-order-traversal-ii.md)

---

Challenge of using only one queue is that how to "rememer" the elements of each level seperately. Instead of using a cache queue to store next level elements, the actual thing we need care about is the ***size*** of each level, which could using `int size = que.size()` to memorize before each inner-iteration.

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
 // time complexity: O(n)
 // space complexity: O(n)
 
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Level order a list of lists of integer
     */
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        if (root == null) {
            return new ArrayList<ArrayList<Integer>> ();
        }

        Queue<TreeNode> que = new LinkedList<TreeNode> ();
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>> ();

        que.offer(root);

        while(!que.isEmpty()) {
            ArrayList<Integer> list = new ArrayList<Integer> ();
            int size = que.size();

            for (int i = 0; i < size; i ++) {
                TreeNode curt = que.poll();

                if (curt.left != null) {
                    que.offer(curt.left);
                }
                if (curt.right != null) {
                    que.offer(curt.right);
                }

                list.add(curt.val);
            }

            res.add(list);
        }

        return res;
    }
}
```

---

- [prev: 068. Binary Tree Postorder Traversal](068-binary-tree-postorder-traversal.md)
- [next: 070. Binary Tree Level Order Traversal II](070-binary-tree-level-order-traversal-ii.md)
