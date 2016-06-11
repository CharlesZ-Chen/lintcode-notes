[106. Convert Sorted List to Balanced BST](http://www.lintcode.com/problem/convert-sorted-list-to-balanced-bst)

- [prev: 105. Copy List with Random Pointer](105-copy-list-with-random-pointer.md)
- [next: 107. Word Break](107-word-break.md)

---

## One time pass! Vola!

```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
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
     * @param head: The first node of linked list.
     * @return: a tree node
     */
    public TreeNode sortedListToBST(ListNode head) {  
        if (head == null) {
            return null;
        }

        ListNode left, mid, right;

        left = getPreMiddle(head);
        mid = left == null ? head : left.next;
        right = mid.next == null ? null : mid.next;

        TreeNode root = new TreeNode(mid.val);

        if (left != null) {
            left.next = null;
            root.left = sortedListToBST(head);
        } else {
            root.left = null;
        }

        if (right != null) {
            mid.next = null;
            root.right = sortedListToBST(right);
        }

        return root;
    }

    public ListNode getPreMiddle(ListNode head) {
        assert head != null;

        ListNode prev = null, slow = head, fast = head.next;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        return prev;
    }
}

```

---

- [prev: 105. Copy List with Random Pointer](105-copy-list-with-random-pointer.md)
- [next: 107. Word Break](107-word-break.md)
